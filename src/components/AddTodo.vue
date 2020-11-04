<template>
  <div>

<form @submit="addTodo">

<input type="text" name="title" v-model="title"
placeholder="Add Todo..">

<input type="submit" value="Add" class="btn">


</form>

  </div>
</template>

<script>
// import uuid from 'uuid';
import { v4 as uuidv4 } from 'uuid'; /*https://www.npmjs.com/package/uuid */

export default {

    name: "AddTodo",

    data(){
        return{
            title:''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault(); //not to refresh

            if (this.title.trim() !== ''){ //* +

                const newTodo = {
                id: uuidv4(),
                title: this.title,
                completed: false
             }

               this.$emit('add-todo', newTodo);
               this.title = '';  //clear the input field
            }

        }
    }

}
</script>

<style scoped>
form {
    display: flex;  /* to align */
  }

  input[type="text"] {
    flex: 10;
    padding: 5px;
  }

  input[type="submit"] {
    flex: 2;
  }
</style>