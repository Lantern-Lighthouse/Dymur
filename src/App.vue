<script setup>
import { ref } from 'vue'

const username = ref('John Pork')
const userstatus = ref(1)

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
</script>

<template>
  <h1 class="text-9xl text-lime-500 placecontent-center-safe">Lantern</h1>
  <h2 class="text-5xl">Welcome, {{ username }}</h2>
  <p v-if="userstatus === 1" class="text-2xl">Online</p>
  <p v-else class="text-2xl">Offline</p>
  <button @click="toggleStatus" class="bg-lime-300 border-2 border-lime-400">Balls</button>
</template>
