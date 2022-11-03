

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
    async fetchdata(){
     const res = await fetch('http://localhost:5000/tasks');
     const data = await res.json();
     return data;
    }
  },
  data() {
    return {
      tasks: [], showAddTask :false
    };
  },
  async created() {
    this.tasks =await this.fetchdata();
  },
};
</script>
<!-- ================================== -->

<style>
@import "./assets/css/style.css";
</style>
