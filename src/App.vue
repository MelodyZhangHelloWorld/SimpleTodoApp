<template>
  <div id="app">
   <TodoList :todo-list=todos />
   
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
   }
}
</script>

<style>

</style>
