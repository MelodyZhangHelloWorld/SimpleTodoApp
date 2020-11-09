<template>
  <div>
    <div :key=todo.id v-for="todo in todoList" >
     
    <TodoItem  :todo="todo" 
    @del-todo="$emit('del-todo', todo.id)"
    />

    </div> 
  </div>

</template>

<script>

import TodoItem from './TodoItem';
export default {
  name: "TodoList",

   components:{
     TodoItem
 },
  props:["todoList"]
 
}
</script>

<style scoped>

</style>

