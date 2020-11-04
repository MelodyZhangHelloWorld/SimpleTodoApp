<template>
  <div id="app">
   <TodoList :todo-list=todos 
   
   @del-todo="deletTodo" 
   />
   
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  },
   data(){
     return{
       todos:[
          {
            id:1,
            title: "Todo One",
            completed: false
          },
           {
            id:2,
            title: "Todo Two",
            completed: true
          },
           {
            id:3,
            title: "Todo Three",
            completed: true
          }

       ]
     }
   },
   methods:{
     deletTodo(id){
       this.todos = this.todos.filter(
         todo => todo.id !== id  ); //* 
     }
   }
}
</script>

<style>

</style>
