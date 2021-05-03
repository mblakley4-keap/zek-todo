<template>
    <div id="app">
      <h1>todos</h1>
      <todo-list :todos="todos"></todo-list>
    </div>
</template>

<script>
import TodoList from "./components/TodoList";

export default {
    name: "App",
    components: {
        TodoList,
    },
    data() {
        return {
          todos: [
            {
              title: 'Todo A',
              project: 'Project A',
              done: false,
            },
            {
              title: 'Todo B',
              project: 'Project B',
              done: false,
            },
            {
              title: 'Todo C',
              project: 'Project C',
              done: false,
            },
            {
              title: 'Todo D',
              project: 'Project D',
              done: false,
            }
          ]
        };
    },
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
