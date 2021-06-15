<template>
    <div>
        <todo 
            v-for="(todo, i) in todos" 
            :key="i" 
            :todo="todo"
            v-on:delete-todo="deleteTodo"
            v-on:complete-todo="completeTodo"
        />
        
    </div>
</template>

<script>
import Todo from './Todo';

export default {
    props: ["todos"],
    components: {
        Todo,
    },
    methods: {
        deleteTodo(todo) {
            const todoIndex = this.todos.indexOf(todo);
            this.todos.splice(todoIndex, 1);
        },
        
        completeTodo(todo) {
            const todoIndex = this.todos.indexOf(todo);
            this.todos[todoIndex].done = !this.todos[todoIndex].done;
        }
    }
};
</script>

<style>
</style>
