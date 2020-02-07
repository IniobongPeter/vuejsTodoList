<template>
  <div class="container">
    <div class="page-header">
      <h3>Vue.js Todo List</h3>
    </div>
    <app-todolist/> 
    
  </div>
</template>

<script>
import ToDoList from '@/components/ToDoList.vue'

export default {
  name: 'app',
  components: {
    'app-todolist': ToDoList 
  }
}
</script>

<style>

</style>