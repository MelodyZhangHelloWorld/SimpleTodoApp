<template>
  <div>
    <div :key=todo.id v-for="todo in todoList" >
     
    <TodoItem  :todo ="todo" 
    
    @del-todo="$emit('del-todo', $event)"
    @mark-complet="$emit('mark-complet', $event )"

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
  props:["todoList"],

   emits: ["mark-complet"]
 
}
</script>

<style scoped>

  .is-complete {
    text-decoration: line-through;
  }

</style>

