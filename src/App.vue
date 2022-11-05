

<template>
  <div class="container">
    <Header title="Task Tracker" @toggle-add-task="toggleAddTask" :showAddTask='showAddTask' />
    <div v-if="this.showAddTask">
      <AddTask @add-task='addTask' />
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
    Tasks, AddTask
  },
  methods: {
    async deleteTask(id) {
      if (confirm('Are you sure !')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })
        res.status === 200 ? this.tasks = this.tasks.filter((task) => task.id !== id) : alert('error deleteing task');
      }
    },
    // =====================================
    async toggleTask(id) {
      const tasktoUPT = await this.fetchdatabyid(id);
      const updatetask = { ...tasktoUPT, reminder: !tasktoUPT.reminder };
      //send data to api 
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updatetask)
      });
      const data = await res.json();
      // update current list 
      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder : data.reminder } : task);
    },
    // =====================================
    async addTask(newtask) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(newtask)
      })
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },

    // =====================================

    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    async fetchdata() {
      const res = await fetch('api/tasks');
      const data = await res.json();
      return data;
    },
    async fetchdatabyid(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    }
  },
  data() {
    return {
      tasks: [], showAddTask: false
    };
  },
  async created() {
    this.tasks = await this.fetchdata();
  },
};
</script>
<!-- ================================== -->

<style>
@import "./assets/css/style.css";
</style>
