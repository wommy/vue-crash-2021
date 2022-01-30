<script setup>
import Task from './Task.vue'
defineProps({
	tasks: Array,
})
defineEmits(['delete-task','toggle-reminder'])
</script>
<template>
	<div v-for="task in tasks">
		<Task 
			:task="task" 
			@delete-task="$emit('delete-task', task.id)"
			@toggle-reminder="$emit('toggle-reminder', task.id)"
		/>
	</div>
</template>
<style scoped>
</style>