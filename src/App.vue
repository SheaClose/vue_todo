<template>
  <div id="app">
    {{msg}}
    <form v-show="!edit" @submit.prevent="submitTodo">
      <label for="new-todo">New Todo:</label>
      <input type="text" name="new-todo" v-model="newTodo" placeholder="Add New Todo" />
    </form>
    <form v-show="edit" @submit.prevent="editTodo">
      <label for="edit-todo">Edit Todo:</label>
      <input type="text" name="edit-todo" v-model="editTodoInput" placeholder="EditTodo" />
    </form>
    
    <list 
      @toggle-edit="toggleEdit"
      @complete-todo="completeTodo" 
      @delete-todo="deleteTodo" 
      :todos='todos'
    >
    </list>
  </div>
</template>

<script>
import list from "./List.vue";
export default {
  data() {
    return {
      editIndex: -1,
      edit: false,
      newTodo: "",
      editTodoInput: "",
      msg: "Welcome to Another freakin' Todo List",
      todos: [
        { complete: false, title: "Display todos" },
        { complete: false, title: "Create new todos" },
        { complete: false, title: "Complete Todos" },
        { complete: false, title: "Delete Todos" },
        { complete: false, title: "Edit Todos" }
      ]
    };
  },
  methods: {
    completeTodo(i) {
      this.todos[i].complete = !this.todos[i].complete;
    },
    deleteTodo(i) {
      this.todos.splice(i, 1);
    },
    submitTodo() {
      this.todos.push({ complete: false, title: this.newTodo });
      this.newTodo = "";
    },
    editTodo() {
      this.todos[this.editIndex].title = this.editTodoInput;
      this.todos[this.editIndex].complete = false;
      this.editIndex = -1;
      this.edit = false;
    },
    toggleEdit(i) {
      this.editIndex = i;
      this.edit = true;
      this.editTodoInput = this.todos[i].title;
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 10px;
}

a {
  color: #42b983;
}
</style>
