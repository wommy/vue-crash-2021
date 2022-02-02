<script setup>
import { reactive, ref } from 'vue'
const emit = defineEmits(['add-task'])
const text = ref('')
const day = ref('')
const reminder = ref(false)

const onSubmit = ()=> {
  if(!text.value) {
    alert('Please add a task')
    return
  }
  
  emit('add-task', reactive({ text, day, reminder }))

  text.value = ''
  day.value = ''
  reminder.value = false
}
</script>
<template>
  <form 
		class="add-form"
		@submit.prevent="onSubmit"
	>
    <div class="form-control">
      <label>Task</label>
      <input 
				type="text" name="text" placeholder="Add Task" 
				v-model="text"
			/>
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text" name="day" placeholder="Add Day & Time"
				v-model="day"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input 
				type="checkbox" name="reminder" 
				v-model="reminder"
			/>
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>
<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>