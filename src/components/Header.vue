<template>
    <header>
        <h1>{{title}}</h1>
    <Button :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'"  
    @btn-click="$emit('toggle-add-task')"/>  
 </header>
 
</template>
<!-- =========================== -->
<script>
import Button from './Button'

export default {
    name: 'Header',
    props:{
        title : String,showAddTask : Boolean
    },
    components:{
        Button
    }
}

</script>
<!-- ========================== -->
<style scoped>
@import '../assets/css/header.css';
</style>