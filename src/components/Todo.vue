<template>
    <div class="card">
        <div class="content" v-show="!isEditing">
            <div class="header">
                {{ todo.title }}
            </div>

            <div class="meta">
                {{ todo.description }}
            </div>

            <div class="extra-content">
                <span class="edit-icon clickable" @click="showForm">
                    ⚙️
                </span>
                <span class="delete-icon clickable" @click="deleteTodo(todo)">
                    ❌
                </span>

            </div>

        </div>

        <div class="content" v-show="isEditing">
            <div class="form">
                <div class="field">
                    <label for="todo.title">Title</label>
                    <input type="text" v-model="todo.title">
                </div>

                <div class="field">
                    <label for="todo.project">Description</label>
                    <input type="text" v-model="todo.description">
                </div>

                <div class="close">
                    <button class="clickable" @click="hideForm">
                        Close
                    </button>
                </div>
            </div>

        </div>


        <div class="status clickable" v-show="todo.done" @click="completeTodo(todo)">
            🟢 Complete
        </div>

        <div class="status clickable" v-show="!todo.done" @click="completeTodo(todo)">
            🔴 Not Complete
        </div>

    </div>
</template>

<script>
export default {
    props: ["todo"],
    data () {
        return {
            isEditing: false,
        };
    },
    methods: {
        showForm() {
            this.isEditing = true;
        },
        hideForm() {
            this.isEditing = false;
        },
        deleteTodo(todo) {
            this.$emit('delete-todo', todo);
        },
        completeTodo(todo) {
            this.$emit('complete-todo', todo);
        },
    },
};
</script>

<style>
.card {
    margin: 10px auto;
    padding: 5px;
    border: 1px solid green;
    border-radius: 10px;
}
.header {
    font-size: 20px;
    font-weight: 600;
}
.content {
    text-align: left;
}
.extra-content {
    text-align: right;
}
.clickable:hover {
    cursor: pointer;
}
.status {
    text-align: left;
}
.close {
    text-align: right;
}
input {
    margin: 5px;
    padding: 5px;
    font-size: 16px;
}
label {
    display: block;
}
</style>
