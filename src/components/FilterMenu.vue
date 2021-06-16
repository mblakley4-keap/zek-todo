<template>
    <div class="filter-menu-container">
        <h2>
            {{ this.pending }} {{ this.pending | pluralize }} remaining
        </h2>
        <p>All</p>
        <p :class="{ selected: visibility === 'all'}">Active</p>
        <p>Completed</p>
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

</style>