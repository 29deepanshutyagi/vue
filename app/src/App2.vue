<script setup lang="ts">
import { ref ,onMounted} from 'vue';

const name = ref('John Doe');
const status = ref('pending');
const tasks = ref(['task1', 'task2', 'task3']);
const link='https://www.google.com';
const newTask=ref('');
const toggleStatus = () => {
  if(status.value==='active'){
    status.value='inactive';
    }else if(status.value==='pending'){
      status.value='inactive';
    }
    else{
      status.value='pending';
    }
}
const addTask=()=>{
  if(newTask.value.trim()!==''){
    tasks.value.push(newTask.value);
    newTask.value='';
  }
}
const deleteTask=(index: number)=>{
  tasks.value.splice(index,1);
}
onMounted(async()=>{
  try{
    const res=await fetch('https://jsonplaceholder.typicode.com/posts');
    const data=await res.json();
    tasks.value=data.map((task:any)=>task.title);
    console.log(data);
  }
  catch(err){
    console.log(err);
  }
})

</script>

<template>
  <!-- <h1>Vue Jobs</h1> -->
  <h1>{{ name }}</h1>
  <p v-if="status==='active'">Vue 3 is active awesome</p>
  <p v-else-if="status==='inactive'">Vue 3 is inactive not awesome</p>
  <p v-else>Vue 3  pending awesome</p>
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Add</button>

  </form>
  <h3>Tasks :</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task">
      <span>{{ task }}</span>
    <button @click="deleteTask(index)">
       x
    </button>
  </li>
  </ul>
  <!-- <a v-bind:href="link">Google</a> -->
  <a :href="link">Google</a>
  <br/>
  <!-- <button v-on:click="toggleStatus">Change Status</button>
    -->
  <button @click="toggleStatus">Change Status</button>
  
</template>


