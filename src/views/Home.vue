<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'
import { ref } from 'vue'

defineProps({
  showAddTask: Boolean,
})
const tasks = ref([])
tasks.value = await fetch('api/tasks').then(r => r.json())
const addTask = async task => {
  tasks.value = [...tasks.value, await fetch('api/tasks', {
    method: 'POST',
    headers: {
      'Content-type': 'application/json',
    },
    body: JSON.stringify(task),
  }).then( r => r.json())]
}
const deleteTask = async id => {
  confirm('Are you sure?') && ( await fetch(`api/tasks/${id}`, {
    method: 'DELETE',
  }) ).status === 200 
    ? ( tasks.value = tasks.value.filter(task => task.id !== id) ) 
    : alert('Error deleting task')
}
const toggleReminder = async id => {
  const taskToToggle = await fetch(`api/tasks/${id}`).then( r => r.json() )
  const data = await fetch(`api/tasks/${id}`, {
    method: 'PUT',
    headers: {
      'Content-type': 'application/json',
    },
    body: JSON.stringify({ ...taskToToggle, reminder: !taskToToggle.reminder }),
  }).then( r => r.json() )
  tasks.value = tasks.value.map( task => task.id === id 
    ? { ...task, reminder: data.reminder } 
    : task
  )
}
</script>

<template>
  <AddTask 
    v-show="showAddTask"
    @add-task="addTask"
  />
  <Tasks 
    :tasks="tasks" 
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
  />
</template>
<style scoped>
</style>