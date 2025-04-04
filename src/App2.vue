<script setup>
import {ref, onMounted} from 'vue';

    const name=ref("John Doe");
    const status=ref("active");
    const tasks=ref(["Learn Vue", "Learn React", "Learn Angular"]);
    const newTask=ref("My Task");

    const addTask=()=>{
      if(newTask.value.trim!==''){
           tasks.value.push(newTask.value);
           newTask.value="";
      }
    }
     const toggleStatus=()=>{
      if(status.value==="active"){
      status.value="pending"
     }
     else if(status.value=="pending"){
      status.value="inactive"
     }
     else{
      status.value="active"
     }
     }
 
const deleteTask=(index)=>{
  tasks.value.splice(index,1);  
}
onMounted(async() => {
  try {
    const res=await fetch("https://jsonplaceholder.typicode.com/todos");
    const data=await res.json();
    console.log(data)
      tasks.value=data.map(task=>task.title);
  } catch (error) {
    console.log(error)
  }
})


</script>

<template>
  <form @submit.prevent="addTask" >
<label for="newTask">Add Task</label>
<input type="text" id="newTask" v-model="newTask">
<button type="submit">Submit</button>
</form>
 <h1>{{ name }}</h1>
 <button @click="changeName">Click</button>
<p v-if="status=='active'">Active status</p>
<p v-else-if="status=='pending'">Pending</p>
<p v-else>Inactive</p>

<h3>Tasks:</h3>
<ol>
  <li v-for="(task , index) in tasks" :key="task">
   <span> {{ task }}</span>
   <button @click="deleteTask(index)">Delete</button>
  </li>
</ol>
<!-- <a v-bind:href="link" target="_blank" href="link">Vue Website</a> -->

<br>
<button @click="toggleStatus">Change Status</button>


</template>

<style scoped>
h1{
  color: red;
}
</style>
