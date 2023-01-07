<template>
  <div id="container">
    <h1>Vue 3 Todo App</h1>
    <form @submit.prevent="addNewTodo()">
      <label for="">Write your new todo in the box below</label>
      <input v-model="newTodo" type="text" name="newTodo" />
      <button>Add New Todo</button>
      <button id="mark-all-done-btn" @click="markAllDone">Mark All Done</button>
    </form>
  </div>
  <ul>
    <li v-for="(todo, index) in todos" v-bind:key="todo.id" class="todo">
      <h3 v-bind:class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </h3>
      <div id="center">
        <button id="removeButton" @click="removeTodo(index)">
          Remove Todo
        </button>
      </div>
    </li>
  </ul>
</template>

<script>
import { ref /*reactive*/ } from "vue";

export default {
  setup() {
    console.log("نوشته شده توسط خشایار شمالی");
    // const data = reactive({
    //   newTodo: "",
    //   todos: [],
    // });

    const newTodo = ref("");
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
    };
  },
};
</script>

<style>
#container {
  background-color: blanchedalmond;
  padding: 20px;
  border-radius: 2px;
}
body {
  background-color: aliceblue;
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 50%;
  margin: 0 auto;
}
input,
textarea,
h2,
label,
button,
p,
div,
section,
article,
select {
  display: "block";
  width: 90%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}
h1 {
  text-align: center;
}
h3 {
  padding-top: 50px;
}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
button {
  background-color: rgb(176, 237, 255);
  padding-top: 15px;
  padding-bottom: 15px;
  border: none;
  cursor: pointer;
  border-radius: 2px;
}
button:hover {
  background-color: rgb(121, 215, 255);
}
form {
  text-align: center;
}
label {
  font-size: 22px;
}
#removeButton {
  background-color: rgb(255, 238, 172);
  width: 75%;
  display: flex;
  justify-content: center;
  border-radius: 2px;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
}
#removeButton:hover {
  background-color: rgb(252, 255, 63);
}
#center {
  display: flex;
  justify-content: center;
}
#mark-all-done-btn {
  background-color: aquamarine;
  cursor: pointer;
  font-size: 20px;
  font-weight: 600;
  border-radius: 2px;
}
#mark-all-done-btn:hover {
  background-color: rgb(113, 238, 196);
}
</style>
