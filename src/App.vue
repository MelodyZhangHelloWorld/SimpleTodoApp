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
                        //must be STRING
 db.collection('todoList').doc(id+'').delete().then(function() {
    console.log("Document with id: "+ id + " is successfully deleted!");
        }).catch(function(error) {
          console.error("Error removing document: ", error);
      });

 this.todos = this.todos.filter(todo => todo.id !== id) //*
       
     },

    markComplete(id){
      // console.log(id);   
      // console.log(this.todos[(id-1)].completed);

        db.collection('todoList').doc(id + '').set({
          id: id,
          title: this.todos[(id-1)].title,
          completed: !this.todos[(id-1)].completed
        })

        this.todos[(id-1)] = {
          id: id,
           title: this.todos[(id-1)].title,
          completed: !this.todos[(id-1)].completed
        }

        //?!!!! not a Vue-way have to update the class, just for DOM
          this.todos = [...this.todos, this.todos[(id-1)]];
          this.todos.pop(); 

     },
     
     addTodo(newTodo){ 
        
       newTodo.id= this.todos.length +1,
                           //doc('') --> auto-generated id
       db.collection('todoList').doc(newTodo.id + '').set({  //****
         id: newTodo.id,
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
