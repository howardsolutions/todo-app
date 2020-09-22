<template>
    <div>
        <form @submit = "addToDo">
            <input type="text" v-model = "title" name="title" placeholder="add todo">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
// import uuid from 'uuid';
export default {
    name: 'AddToDo',

    data() {
        return {
            title: ''
        }
    },
    
    methods: {
        addToDo(e) {
            // we dont want the form try to submit to a file
            e.preventDefault();

            const newTodo = {
                title: this.title,
                completed: false
            } 
            // Send event (add new to do) to parent
            this.$emit('add-todo', newTodo)
        }
    }
}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>
