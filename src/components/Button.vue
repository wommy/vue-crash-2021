<script setup>
defineProps({
  text: String,
  color: String,
})
function onClick() {
	console.log('click') 
} 
</script>
<template>
	<button 
		class="btn"
		:style="{background: color}"
		@click="onClick"
	>{{ text }}</button>
</template>
<style>
</style>