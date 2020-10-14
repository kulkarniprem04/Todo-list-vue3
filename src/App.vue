<template>
  <h1>Vue 3 todo app</h1>
  <form @submit.prevent="addNewTodo" class="form">
    <label>Add new todo</label>
    <input v-model="newtodo" class="input" type="text" />
    <button type="submit">Add Todo</button>
  </form>
  <button @click="markAllDone()">Mark all done</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h2 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h2>
      <button @click="removeTodo(index)">Remove todo</button>
    </li>
  </ul>
  <!-- <h2>{{newtodo}}</h2> -->
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newtodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newtodo.value
      });
      newtodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach(todo => (todo.done = true));
    }
    return {
      todos,
      newtodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone
    };
  }
};
</script>

<style>
body {
  font-family: sans-serif;
  text-align: center;
  padding-top: 1em;
  padding-bottom: 1em;
  color: #2c3e50;
  margin: 0 auto;
  width: 80%;
}
/* .form {
  height: 20%;
}
.input {
  width: 60%;
} */
input,
label {
  width: 100%;
  height: 2em;
  display: block;
  width: 100%;
  margin: 0 auto;
}
button {
  cursor: pointer;
  width: 20%;
  height: 3em;
  text-align: center;
  margin-top: 2em;
  border-radius: 8px;
  border: 1px solid black;
  background-color: black;
  color: white;
}
button:hover {
  background-color: white;
  color: black;
}
h2 {
  text-align: left;
}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
