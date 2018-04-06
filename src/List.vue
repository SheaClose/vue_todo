<template>
  <div>
    <ul>
      <li :class='{strike: todo.complete}' :key="i" v-for="(todo, i) in todos">
        {{todo.title}}
        <button @click="todoComplete(i)">-</button>
        <button @click="toggleEdit(i)">o</button>
        <button @click="deleteTodo(i)">x</button>
      </li>
    </ul>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.component("list", {
  data() {
    return {
      items: [1, 2, 3, 4]
    };
  },
  methods: {
    todoComplete(i) {
      this.$emit("complete-todo", i);
    },
    deleteTodo(i) {
      this.$emit("delete-todo", i);
    },
    toggleEdit(i) {
      this.$emit("toggle-edit", i);
    }
  },
  props: {
    todos: {
      type: [Array],
      default: []
    }
  }
});
</script>

<style scoped>
.strike {
  text-decoration: line-through;
}
</style>
