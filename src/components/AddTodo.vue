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

export default {

    name: "AddTodo",
     props:["todoList"],

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
            
                title: this.title,
                completed: false //default setting               
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