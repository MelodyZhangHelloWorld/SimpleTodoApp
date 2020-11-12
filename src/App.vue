<template>
  <div id="app">

   
    <b-row align-h="center" class="m-3">
    <b-col md="7" >
   <Header  />
  <AddTodo  @add-todo="addTodo" />

   <TodoList :todo-list=todos 
   
   @mark-complet="markComplete"
   @del-todo="deleteTodo" 


   />

   
</b-col>
    </b-row>
  </div>
</template>

<script>

import Header from './components/layout/Header';
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';

// import { v4 as uuidv4 } from 'uuid'; /*https://www.npmjs.com/package/uuid */

import db from './components/firebaseInit'; //*



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
 
   created(){
    
      db.collection('todoList').orderBy('id').get().then(
        querySnapshot => {    //*
          querySnapshot.forEach (doc => {
    
           console.log(doc.data());
       //     console.log((new Date()).getTime() );
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

     deleteTodo(id){
        console.log("-------id-----------------");
         console.log(id);
 db.collection('todoList').doc(id +'').delete().then(function() {
    console.log("Document with id: " + id +" is successfully deleted!");
        }).catch(function(error) {
          console.error("Error removing document: ", error);
      });

 this.todos = this.todos.filter(todo => todo.id !== id); //*
       
     },

    markComplete(id){
      console.log("-------id-----------------");
     console.log(id);   
    
    let thisTitle = this.todos.filter(todo => todo.id === id)[0].title; 
    let thisCompleted = this.todos.filter(todo => todo.id === id)[0].completed;
    
        db.collection('todoList').doc(id+'').set({
          id: id,
          title: thisTitle,
          completed: ! thisCompleted
        })
       
  //conventional js
      let i;
    for (i = 0; i < this.todos.length; i ++){
        if (this.todos[i].id == id ){
          this.todos[i].completed = ! thisCompleted;
        }
    }

  console.log(this.todos);
     
     
        }

        
         ,
     
     addTodo(newTodo){ 
      
        const newId = (new Date()).getTime(); //Get the time (milliseconds since January 1, 1970)
        newTodo.id = newId; // how come you forgot this one!
                                 //MUST BE STRING
       db.collection('todoList').doc(newId +'').set({  //****
        
         id: newId,
         title: newTodo.title,
         completed: newTodo.completed
       })

       this.todos.push(newTodo); //for instant update..
      
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
    
      background-color: rgb(222, 245, 226);

  }
  .is-complete {
    text-decoration: line-through;
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
