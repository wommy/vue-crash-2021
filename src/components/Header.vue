<script setup>
import Button from './Button.vue'
defineProps({
  title: String,
	showAddTask: Boolean,
})
defineEmits(['btn-click','toggle-add-task'])
</script>
<template>
	<header>
		<h1>{{ title }}</h1>
		<Button 
			@btn-click="$emit('toggle-add-task')"
			:text="showAddTask ? 'Close' : 'Add Task' "
			:color="showAddTask ? 'red' : 'green' " 
		/>
	</header>
</template>
<style scoped>
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 20px;
	}
</style>