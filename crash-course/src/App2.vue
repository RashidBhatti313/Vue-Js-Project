// <script>
// export default {
//   data() {
//     return {
//       name: 'Rashid Hussain',
//       status: 'pending',
//       tasks: ['Task One', 'Task Two', 'Task Three'],
//       link: 'https://google.com'
//     };
//   },
//   methods: {
//     toggleStatus() {
//       if (this.status === 'active') {
//         this.status = 'pending';
//       } else if (this.status === 'pending') {
//         this.status = 'inactive';
//       } else {
//         this.status = 'active';
//       };
//     },
//   },
// };
// </script>

// <template>
//   <h1>{{ name }}</h1>
//   <p v-if="status === 'active'">User is Active</p>
//   <p v-else-if="status === 'pending'">User is Pending</p>
//   <p v-else>User is InActive</p>

//   <h3>Tasks:</h3>
//   <ul>
//     <li v-for="task in tasks" :key="task.id">
//       {{ task }}
//     </li>
//   </ul>

//   <!-- <a v-bind:href="link">Click for Google</a> -->
//   <a :href="link">Click for Google</a>
//   <br>
//   <!-- <button v-on:click="toggleStatus">Change Status</button> -->
//   <button @click="toggleStatus">Change Status</button>
// </template>


<script setup>
import { onMounted, ref } from 'vue';

const name = ref('Rashid Hussain');
const status = ref('active');
const tasks = ref(['Task One', 'Task Two', 'Task Three']);
const newTask = ref('');


const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map(task => task.title);
  } catch (error) {
    console.log('Error fetching tasks', error);
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is InActive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" name="newTasks" id="newTasks" v-model="newTask" />
    <button type="submit">submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task.id">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <!-- <a v-bind:href="link">Click for Google</a> -->
  <a :href="link">Click for Google</a>
  <br>
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>
</template>

