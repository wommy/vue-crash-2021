<script setup>
defineProps({
  text: String,
  color: String,
})
defineEmits(['btn-click'])
</script>
<template>
	<button 
		class="btn"
		:style="{background: color}"
		@click="$emit('btn-click')"
	>{{ text }}</button>
</template>
<style>
</style>