<script setup>
    // Import BlogPost component 
    //
    import blogPost from './subcomponents/BlogPost2.vue'
    import axios from 'axios'
</script>


<script>
    export default {
        components: {
            blogPost
        },
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname == 'localhost')
                    return 'http://localhost:3000'
                else {
                    const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
            }
        },
        created() { // [translate:created is a hook that executes as soon as Vue instance is created]
            axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
        },
        methods: {
            deletePost(id) {
                // TODO: Complete the delete method
                axios.get(`${this.baseUrl}/deletePost`, {params: {
                    id: id
                }})
                .then(response => {
                    // this gets the data, which is an array
                    console.log(id)
                    this.posts = this.posts.filter(post=>post.id!=id)
                    console.log(response.data)
                })
                .catch(error => {
                    this.posts = [{ entry: 'There was an error: ' + error.message }]
                })
            }
        }
    }
</script>


<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
<blogPost v-for="v in this.posts" :key="v.id" :id="v.id" :mood="v.mood" :subject="v.subject" :entry="v.entry">
    <button class="btn btn-primary" @click="deletePost(v.id)">Delete</button>
</blogPost>
</template>