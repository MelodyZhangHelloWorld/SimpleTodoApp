<template>
  <div>
    <div :key=todo.id v-for="todo in todoList" >
     
      <h3> {{ todo.title}} </h3>
    

    </div>
  </div>
</template>

<script>


export default {
  name: "TodoList",

   components:{
     
 },
  props:["todoList"]
 
}
</script>

<style scoped>

</style>

