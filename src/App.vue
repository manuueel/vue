<script>
import { defineComponent } from 'vue'
import ToDo from './components/ToDo.vue'

export default defineComponent({
  name: 'App',
  components: {
    ToDo
  },
})
</script>

<template>
  <div id="app">
    <img class="logo" src="@/assets/vite.svg" alt="Vite logo" />
    <img class="logo" src="@/assets/vue.svg" alt="Vue logo" />
    <ToDo title="To-Do List" />
  </div>
</template>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vanilla:hover {
  filter: drop-shadow(0 0 2em #f7df1eaa);
}
</style>
