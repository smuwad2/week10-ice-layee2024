<script>
    // TODO: Complete the code
    export default { 
        data() {
            return {
                
            }
        },
        // Hint: insert properties task (Object) and idx (Number)
        props: {
            desc: String,
            deadline: String,
            idx: Number
        }
    }
</script>

<template>
    <div class="card" style="width: 18rem;">
        <div class="card-body">
            <h5 class="card-title">Deadline: {{ deadline }}</h5>
            <p class="card-text">{{ desc }}</p>
            <button class="btn btn-primary" @click="$emit('deleteTask')">Done</button>
        </div>
    </div>
</template>


