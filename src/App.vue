<template>
    <div id="app">
      <h1>todos</h1>
      <create-todo v-on:add-todo='addTodo'></create-todo>
      <section class="main-container" v-show="todos.length">
        <filter-menu :todos="todos"></filter-menu>
        <todo-list :todos="todos"></todo-list>
      </section>
    </div>
</template>

<script>
import TodoList from "./components/TodoList";
import CreateTodo from "./components/CreateTodo";
import FilterMenu from "./components/FilterMenu";

const TODO_STORE_KEY = "mikeLocalVueStore2021";

export default {
    name: "App",
    components: {
        FilterMenu,
        TodoList,
        CreateTodo,
    },
    data() {
        return {
          todos: [],
        };
    },

    mounted() {
      this.init();
    },

    watch: {
      todos(todos) {
        localStorage.setItem(TODO_STORE_KEY, JSON.stringify(todos))
      },
    },

    methods: {
      init() {
        const todos = JSON.parse(localStorage.getItem(TODO_STORE_KEY) || []);
        todos.forEach((todo, i) => {
          todo.id = i;
        });
        this.todos = todos;
      },

      addTodo(title) {
        this.todos.push({
          id: this.todos.length + 1,
          title,
          done: false,
        });
      },
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
    box-sizing: border-box; 
}

h1 {
  font-size: 4em;
  font-weight: 200;
  margin-bottom: .25em;
}

.main-container {
  margin: 1em auto;
  text-align: left;
  width: 80%;
  display: grid;
  grid-template-columns: 35% 65%;
  column-gap: 1em;
}
</style>
