<script >
export default{
  data(){
    return {
      name:"John Doe",
      status: "inactive",
      tasks:["Learn Vue", "Learn React", "Learn Angular"],
      link: "https://vuejs.org/"
    }
  
  },
  methods: {
    changeName() {
      this.name="Ram"
    },
    toggleStatus(){
     if(this.status=="active"){
      this.status="pending"
     }
     else if(this.status=="pending"){
      this.status="inactive"
     }
     else{
      this.status="active"
     }
    }
  },
}
</script>

<template>
 <h1>{{ name }}</h1>
 <button @click="changeName">Click</button>
<p v-if="status=='active'">Active status</p>
<p v-else-if="status=='pending'">Pending</p>
<p v-else>Inactive</p>

<h3>Tasks:</h3>
<ul>
  <li v-for="task in tasks" :key="task">
    {{ task }}
  </li>
</ul>
<!-- <a v-bind:href="link" target="_blank" href="link">Vue Website</a> -->
<a :href="link" target="_blank" href="link">Vue Website</a>
<br>
<button @click="toggleStatus">Change Status</button>
</template>

<style scoped>
h1{
  color: red;
}
</style>
