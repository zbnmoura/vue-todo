<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todo";
import AddTodo from "../components/AddTodo";

export default {
  name: "Home",
  components: { Todos, AddTodo },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      fetch(`https://jsonplaceholder.typicode.com/posts/${id}`, {
        method: "DELETE"
      });

      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(new_todo) {
      console.log("11111111111111111", new_todo);
      const { title, completed } = new_todo;
      console.log("xxxxxxxxxxxxxxxxxx", { title, completed });
      fetch("https://jsonplaceholder.typicode.com/posts", {
        method: "POST",
        body: JSON.stringify({
          title: "aaaaaaaaaaaaaaaaa",
          completed: false
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8"
        }
      })
        .then(response => response.json())
        .then(json => (this.todos = [...this.todos, json]));
      // fetch("https://jsonplaceholder.typicode.com/todos", {
      //   method: "POST",
      //   body: JSON.stringify({
      //     title,
      //     completed
      //   }),
      //   headers: {
      //     "Content-type": "application/json; charset=UTF-8"
      //   }
      // })
      //   .then(response => {
      //     console.log("222222222222222222222", response);
      //     return response.json();
      //   })
      //   .then(json => {
      //     console.log("3333333333333333333", json);
      //     this.todos = [...this.todos, json];
      //   })
    }
  },
  created() {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then(response => response.json())
      .then(json => (this.todos = json))
      .catch(e => console.error(e));
  }
};
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
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
</style>
