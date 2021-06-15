<template>
    <div id="app">
      <h1>todos</h1>
      <create-todo v-on:add-todo='addTodo'></create-todo>
      <todo-list :todos="todos"></todo-list>
    </div>
</template>

<script>
import TodoList from "./components/TodoList";
import CreateTodo from "./components/CreateTodo";

export default {
    name: "App",
    components: {
        TodoList,
        CreateTodo,
    },
    data() {
        return {
          todos: [
            {
              title: 'Todo A',
              description: 'the first todo',
              done: false,
            },
            {
              title: 'Todo B',
              description: 'the second todo',
              done: false,
            },
            {
              title: 'Todo C',
              description: 'the third todo',
              done: false,
            },
            {
              title: 'Todo D',
              description: 'the fourth todo',
              done: false,
            }
          ]
        };
    },

    methods: {
      addTodo(payload) {
        const { title, description = "" } = payload;
        this.todos.push({
          title,
          description,
          done: false,
        })
      }
    }
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
    margin-top: 60px;
}
</style>
