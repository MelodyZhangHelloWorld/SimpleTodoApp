<template>
  <div id="app">
    <Header  />
    <AddTodo  @add-todo="addTodo" />
   <TodoList :todo-list=todos 
   
   @del-todo="deletTodo" 
   />
   
  </div>
</template>

<script>

import Header from './components/layout/Header'
import TodoList from './components/TodoList.vue'
import AddTodo from './components/AddTodo.vue'

export default {
  name: 'App',
  components: {
    Header,
    TodoList,
    AddTodo
    

  },
   data(){
     return{
       todos:[
          {
            id:1,
            title: "Todo One",
            completed: true
          },
           {
            id:2,
            title: "Todo Two",
            completed: true
          },
           {
            id:3,
            title: "Todo Three",
            completed: false
          }

       ]
     }
   },
   methods:{
     deletTodo(id){
       this.todos = this.todos.filter(
         todo => todo.id !== id  ); //* 
     },
     addTodo(newTodo){
        this.todos = [...this.todos, newTodo];
     }
   }
}
</script>

<style>

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }


</style>
