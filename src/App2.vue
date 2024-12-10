<script setup>

import { ref } from 'vue';
import { onMounted } from 'vue';

const name = ref('John Doe')
const status = ref('active')
const tasks = ref(['Task 1', 'Task 2', 'Task 3'])
const newTask = ref('')
const socialLinks = ref([
  { name: 'Twitter', url: 'https://twitter.com/johndoe' },
  { name: 'GitHub', url: 'https://github.com/johndoe' },
  { name: 'LinkedIn', url: 'https://linkedin.com/johndoe' },
])
const toggleStatus = () => {
  status.value = status.value === 'active' ? 'pending' : 'active'
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async() => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.map(task => task.title)
  } catch (error) {
    
    console.log('Error fetching tasks:', error)
  }
  
})
</script>

<template>
  <div>
    <h1> {{ name }}</h1>
    <div v-if="status === 'active'">User is Active</div>
    <div v-else-if="status === 'pending'">User is Pending</div>
    <div v-else>User is inactive</div>


    <form @submit.prevent="addTask">
      <label for="task">Add task</label>
      <input type="text" id="newtask" v-model="newTask">
      <div class="flex gap-5">
        <button type="submit">Add</button>
        
      </div>
    </form>

    <ul>
      <li v-for="task in tasks" :key='task'> {{ task }} <button type="button" @click="deleteTask">X</button></li>
    </ul>

    <ul>
      <li v-for="link in socialLinks" :key="link.name"> <a :href="link.url">{{ link.name }} </a></li>
    </ul>

    <button @:click="toggleStatus"> Toggle Status</button>


  </div>
</template>

<style scoped>
div,
h1,
ul {
  background-color: #3b5998;
  color: #fff;
  padding: 20px;
}

ul {
  display: flex;
  flex-direction: column;
  gap: 20px;  
  padding: 10px;
  font-size: 17px
}

button {
  background-color: #3b5998;
  color: #fff;
  padding: 10px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  font-size: 17px;
}

form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 20px;
}

label {
  margin-bottom: 10px;
  font-size: 17px;
}

input {
  background-color: #f5f5f5;
  border: 1px solid #3b5998;
  padding: 10px;
  border-radius: 10px;
  outline: none;
  font-size: 17px;
  margin-bottom: 20px;
}

a {
  color: #3b5998;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
