<template>
  <div id="app">

   
    <b-row align-h="center" class="m-3">
<b-col md="8" >
   <Header  />
  <AddTodo  @add-todo="addTodo" />
   <TodoList :todo-list=todos 
   
   @del-todo="deletTodo" 
   />
</b-col>
    </b-row>
  </div>
</template>

<script>

import Header from './components/layout/Header';
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';

import db from './components/firebaseInit'; //*
//**
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    TodoList,
    AddTodo

  },
   data(){
     return{
       todos:[],
       item:''
       
     }
   },
 //* http request */
   created(){
  
      
      db.collection('todoList').get().then(
        querySnapshot => {

          querySnapshot.forEach (doc => {

          //  console.log(doc.data());

            const item ={
              'id': doc.data().id,
              'title': doc.data().title,
              'completed': doc.data().completed
            }
            
            this.todos.push(item);
           
          })
        }

      )
      
    },

   methods:{

     deletTodo(id){

       axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
       .then(
         res => 
         this.todos = this.todos.filter(
         todo => todo.id !== id,//*
         console.log(res.data))//...?
         
       ).catch(error => console.log(error) ); 


        
     },
     
     addTodo(newTodo){
        
        /*const {id, title, completed} = newTodo; //** 
        
        axios.post('https://jsonplaceholder.typicode.com/todos', {id, title, completed})
        .then(    
         res => 
          this.todos = [...this.todos, res.data],//*
          console.log(this.todos)

        )
        .catch(error => console.log(error) );  */

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
      width: 100%;
    
      

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
