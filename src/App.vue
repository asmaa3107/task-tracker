

<template>
  <div class="container">
    <Header title="Task Tracker" @toggle-add-task="toggleAddTask" :showAddTask='showAddTask'/>  
    <div v-if="this.showAddTask">
      <AddTask @add-task='addTask'/>
    </div>
    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleTask" :tasks="tasks" />
    <Footer />
  </div>
</template>
<!-- ================================= -->
<script>
import Header from "./components/Header";
import Footer from "./components/Footer";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask.vue";
export default {
  name: "App",
  components: {
    Header,
    Footer,
    Tasks,AddTask
  },
  methods: {
   
    deleteTask(id) {
      if (confirm('Are you sure !')) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleTask(id) {
       this.tasks = this.tasks.map((task) => (task.id === id) ? {...task , reminder: !task.reminder } : task) ;
    },
    addTask(newtask){
      this.tasks = [...this.tasks , newtask]; 
      // this.tasks.push(newtask);
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
  },
  data() {
    return {
      tasks: [], showAddTask :false
    };
  },
  created() {
    this.tasks = [
      { id: 1, text: "dotor appointment", day: "Marh 1st at 2:30", reminder: true },
      { id: 2, text: "Grocery shopping", day: "April 1st at 2:30", reminder: true },
      { id: 3, text: "Hangout with freinds", day: "Augest 1st at 2:30", reminder: false },
    ];
  },
};
</script>
<!-- ================================== -->

<style>
@import "./assets/css/style.css";
</style>
