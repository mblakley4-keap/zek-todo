<template>
    <div class="filter-menu-container">
        <h2>
            {{ this.pending }} {{ this.pending | pluralize }} remaining
        </h2>
        <p>
            <a 
                href="#/all" 
                :class="{ selected: visibility === 'all'}"
                class="clickable" 
                @click="filterTodoList('all')"
            >
                All
            </a>
        </p>
        
        <p>
            <a 
                href="#/active"
                :class="{ selected: visibility === 'active'}"
                class="clickable"
                @click="filterTodoList('active')"
            >
                Active
            </a>
        </p>

        <p>
            <a 
                href="#Completed"
                :class="{ selected: visibility === 'completed'}"
                class="clickable"
                @click="filterTodoList('completed')"
            >
                Completed
            </a>
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
        color: #2c3e50 !important;
        text-decoration: underline !important;
        font-weight: 500;
    }

    a:link, a:visited {
        color: #A3BAC3;
        text-decoration: none;
    }

    a:hover {
        cursor: pointer;
        color: #2c3e50;
    }

</style>