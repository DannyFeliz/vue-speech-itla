<template>
  <div id="app" class="container">
    <h1>{{ title }} ({{ tasks.length }})</h1>
    <p>Completed: ({{ completedTasks.length }})</p>
    <p>Incompleted: ({{ incompletedTasks.length }})</p>
    <p v-if="tasks.length == completedTasks.length">
        Congratulations 🎉! you completed all yours tasks
    </p>
    <p v-else>
        You have pending tasks
    </p>
    <ul>
      <li v-for="task, index in tasks" :class="{ 'completed-task': task.completed}" class="pointer">
        <span @click="toggleTask(index)">
          {{ task.completed ? '✓' : '▢' }} {{ task.description }} - {{ task.created_at | formatDate }}
        </span>
        <button @click="removeTask(index)">×</button>
      </li>
    </ul>

    <input type="text" v-model.trim="newTask" @keyup.enter="addTask()">

    <button @click="addTask()" :disabled="!newTask" :title='!newTask ? "Fill the box to add a new todo" : ""'>
      Add Task
    </button>

    <br>
    <br>
    <alert message="This is my message"></alert>
    <alert :message="title" type="danger" :closable="true"></alert>

    <div v-for="user in users" class="row">
      <card :data="user"></card>
    </div>

  </div>
</template>

<script>
import moment from "moment";
import alert from "./components/alert.vue"
import card from "./components/card.vue"

export default {
  name: 'app',
  components: {
    alert,
    card
  },
  data () {
    return {
      title: 'Your Taks',
      newTask: "",
      tasks: [
        { description: "Go the store", completed: false, created_at: moment().subtract("minutes", 15)},
        { description: "Pay the bills", completed: true, created_at: moment().subtract("minutes", 50) },
        { description: "Buy some food", completed: false, created_at: moment().subtract("hours", 1)},
        { description: "Be awesome today", completed: true, created_at: moment().subtract("days", 2)}
      ],
      users: []
    }
  },
  created() {
      this.getUsers();
  },
  filters: {
    formatDate(date) {
        return moment(date).format("DD MMM YYYY [at] hh:mm:ss a");
    }
  },
  computed: {
    completedTasks() {
        return this.tasks.filter(task => task.completed);
    },
    incompletedTasks() {
        return this.tasks.filter(task => !task.completed);
    }
  },
  methods: {
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed
    },
    addTask() {
      if (!this.newTask) return "";
      this.tasks.push({ description: this.newTask, completed: false, create_at: new Date() });
      this.newTask = "";
    },
    removeTask(index) {
      if (confirm("Are you sure?")) {
        this.tasks.splice(index, 1);
      }
    },
    getUsers() {
      axios({
        url: "https://randomuser.me/api/?results=5&nat=es",
        method: "GET"
      }).then(users => {
          this.users = users.data.results;
      })
    }
  }
}
</script>

<style lang="scss">
.pointer {
  cursor: pointer;
}
.completed-task {
  text-decoration: line-through;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  // display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
