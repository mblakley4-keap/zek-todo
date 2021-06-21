<template>
    <div class="card">
        <div class="content" v-show="!editing">
            <input type="checkbox" class="circle" @click="completeTodo(todo)" v-model="todo.done" />
            <label >{{ todo.title }}</label>
            <button class="delete" @click="deleteTodo(todo)">X</button>
        </div>

        <div class="content" v-show="editing">
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
    </div>
</template>

<script>
export default {
    props: ["todo"],
    data () {
        return {
            editing: false,
        };
    },
    methods: {
        showForm() {
            this.editing = true;
        },
        hideForm() {
            this.editing = false;
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
    margin: 0 auto 5px;
    padding: 10px;
    border: 1px solid #EAEBED;
    border-radius: 10px;
}

.circle {
    width: 2em;
    height: 2em;
    border-radius: 50%;
    vertical-align: middle;
    border: 1px solid #ddd;
    -webkit-appearance: none;
    outline: none;
    cursor: pointer;
}

.circle:checked {
    background: #A3BAC3;
}


.content {
    display: grid;
    grid-template-columns: 10% 80% 10%;
    font-size: 1.5em;
}

.clickable:hover, .delete:hover {
    cursor: pointer;
}

.delete {
    color: rgb(182, 79, 79);
    border: none;
    font-weight: 600;
    font-size: 1em;
    background-color: white;
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
