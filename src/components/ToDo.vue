<template>
  <div>
    <h1>To Do List</h1>
    <nav class="task-filter-nav">
      <button @click="currentFilter = 'all'" :class="{ active: currentFilter === 'all' }">All</button>
      <button @click="currentFilter = 'completed'" :class="{ active: currentFilter === 'completed' }">Completed</button>
      <button @click="currentFilter = 'incomplete'" :class="{ active: currentFilter === 'incomplete' }">Incomplete</button>
    </nav>
    <div class="task-enter">
      <input class="task-enter-input" v-model="newTask" placeholder="Enter a new task" @keyup.enter="addTask">
      <button @click="addTask">Add Task</button>
    </div>
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index" class="task" :class="{ 'task-completed': task.completed }">
        <span class="task-span">{{ task.description }}</span>
        <input type="checkbox" v-model="task.completed">
        <button class="task-button-remove" @click="removeTask(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentFilter: 'all',
      newTask: '',
      tasks: []
    };
  },
  computed: {
    filteredTasks() {
      switch (this.currentFilter) {
        case 'completed':
          return this.tasks.filter(task => task.completed);
        case 'incomplete':
          return this.tasks.filter(task => !task.completed);
        default:
          return this.tasks;
      }
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ description: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTaskCompleted(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    }
  }
};
</script>

<style lang="scss">
body {
  font-family: 'Arial', sans-serif;
  background-color: #121212;
  color: #E0E0E0;
  text-align: center;

  #app {
    margin: 0 auto;
    width: 44%;
    color: #BDBDBD;

    .task-enter {
      display: flex;
      justify-content: space-between;
  
      .task-enter-input {
        width: 80%;
        background-color: #333;
        color: #E0E0E0;
        border: 1px solid #424242;
      }
    }
  
    .task-span {
      width: 80%;
      text-align: left;
      color: black;
    }
  
    .task-filter-nav {
      display: flex;
      justify-content: center;
      margin-bottom: 20px;
  
      button {
        margin: 0 10px;
        padding: 10px 20px;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s;
  
        &:hover {
          background-color: #0056b3;
        }
  
        &.active {
          background-color: #ffc107;
          color: black;
        }
      }
    }
  
    ul {
      list-style: none;
      padding: 0;
  
      li {
        background-color: white;
        margin: 10px 0;
        padding: 10px 20px;
        border-radius: 5px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        display: flex;
        align-items: center;
        justify-content: space-between;
  
        &.task-completed {
          .task-span {
            text-decoration: line-through;
            color: #888;
          }
        }
      }
    }
  
    input[type="checkbox"] {
      margin-right: 20px;
    }
  
    input[type="text"] {
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      width: calc(100% - 22px);
      margin-bottom: 20px;
    }
  
    button {
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px 20px;
      cursor: pointer;
      transition: background-color 0.3s;
  
      &:hover {
        background-color: #218838;
      }
  
      &.remove-btn {
        background-color: #dc3545;
  
        &:hover {
          background-color: #c82333;
        }
      }
    }
  }
}
</style>