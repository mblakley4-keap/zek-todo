<template>
    <div class="filter-menu-container">
        <h2>
            {{ this.pending }} {{ this.pending | pluralize }} remaining
        </h2>
        <p 
            :class="{ selected: visibility === 'all'}"
            class="clickable"
            @click="filterTodoList('all')"
        >
            All
        </p>
        
        <p 
            :class="{ selected: visibility === 'active'}"
            class="clickable"
            @click="filterTodoList('active')"
        >
            Active
        </p>

        <p 
            :class="{ selected: visibility === 'completed'}"
            class="clickable"
            @click="filterTodoList('completed')"
        >
            Completed
        </p>
  </div>
</template>

<script>
export default {
    props: ["todos", "visibility"],

    computed: {
        completed() {
            return this.todos.filter((todo) => {
                return todo.done === true;
            }).length
        },

        pending() {
            return this.todos.filter((todo) => {
                    return todo.done === false;
            }).length
        },
    },

    methods: {
        filterTodoList(status) {
            this.$emit('filter-todo-list', status);
        },
    },

    filters: {
        pluralize(x) {
            return x === 1 ? "task" : "tasks"
        }
    }
}
</script>

<style>
    .filter-menu-container {
        /* box-shadow: 1px 1px 5px .01em #006989;
        border-radius: 10px;
        height: 10vh; */
        padding: 15px;
    }

    .selected {
        color: #2c3e50;
        text-decoration: underline;
        font-weight: 500;
    }

    .clickable:hover {
    cursor: pointer;
    color: #A3BAC3;
}

</style>