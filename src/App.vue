<script setup>
import { onMounted, ref } from 'vue'

const username = ref('John Pork')
const userstatus = ref(1)
const newTask = ref("")
const tasks = ref([])

const toggleStatus = () => {
  switch (userstatus.value) {
    case 1:
      userstatus.value = 2
      break
    default:
      userstatus.value = 1
      break
  }
}

const addTask = () => {
	if(newTask.value.trim() !== '') {
		tasks.value.push(newTask.value)
		newTask.value = ''
	}
}

const deleteTask = (index) => {
	tasks.value.splice(index, 1);
}

onMounted(async () => {
	try {
		const response = await fetch('https://jsonplaceholder.typicode.com/todos');
		const data = await response.json();
		tasks.value = data.map((task) => task.title);
	} catch (error) {
		console.error('Error fetching tasks');
	}
});
</script>

<template>
  <h1>Lantern</h1>
  <h2>Welcome, {{ username }}</h2>
  <p v-if="userstatus === 1">Online</p>
  <p v-else>Offline</p>
  <button @click="toggleStatus">Balls</button>

  <ul>
	<li v-for="(task, index) in tasks" :key="task">
		<span>
			{{ task }}
		</span>
		<button @click="deleteTask(index)">x</button>
	</li>
  </ul>

  <form @submit.prevent="addTask">
	<label for="newTask">Add task</label>
	<input type="text" id="newTask" name="newTask" v-model="newTask"></input>
	<input type="submit"></input>
  </form>
</template>
