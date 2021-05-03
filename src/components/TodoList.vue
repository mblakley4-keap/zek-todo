<template>
    <div>
        <p>
            Completed Tasks:
            {{
                todos.filter((todo) => {
                    return todo.done === true;
                }).length
            }}
        </p>
        <p>
            Pending Tasks:
            {{
                todos.filter((todo) => {
                    return todo.done === false;
                }).length
            }}
        </p>
        <todo 
            v-for="todo in todos" 
            :key="todo" 
            :todo="todo"
            v-on:delete-todo="deleteTodo"
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
        }
    }
};
</script>

<style>
</style>
