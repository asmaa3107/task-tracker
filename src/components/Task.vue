<template>
    <div :class="[task.reminder ? 'reminder' : '' , 'task'] ">
        <h3>
            {{ task.text }}
            <i
             @click="$emit('delete-task' , task.id)"
            class="fas fa-times"></i>
        </h3>
        <p>{{ task.day }}</p>
    </div>
</template>
<!-- =============== -->
<script>
export default {
    name: 'Task',
    props: {
        task: Object
    }
}
</script>
<style scoped>
.fas{
    color:red;
}
@import '../assets/css/task.css';
</style>