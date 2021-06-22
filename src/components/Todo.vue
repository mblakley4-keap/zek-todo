<template>
    <div class="card">
        <div class="content" v-show="!editing">
            <input type="checkbox" class="circle" @click="completeTodo(todo)" v-model="todo.done" />
            <label @dblclick="editTodo" :class="{ strike: todo.done }">{{ todo.title }}</label>
            <button class="delete" @click="deleteTodo(todo)">X</button>
        </div>

        <div class="content" v-if="editing">
            <div></div>
            <edit-todo
                :todo="todo"
                v-on:edit-done="editDone"
                v-on:edit-cancel="editCancel"
            />
        </div>

    </div>
</template>

<script>
import EditTodo from './EditTodo'

export default {
    props: ["todo"],

    components: {
        EditTodo,
    },

    data () {
        return {
            editing: false,
        };
    },
    methods: {
        deleteTodo(todo) {
            this.$emit('delete-todo', todo);
        },

        completeTodo(todo) {
            this.$emit('complete-todo', todo);
        },

        editTodo() {
            this.editing = true;
        },

        editDone(editedTitle) {
            const value = editedTitle.trim();
            
            if (!value) {
                this.editing = false;
                return
            }

            this.todo.title = value;
            
            this.editing = false;
        },

        editCancel() {
            this.editing = false;
        }
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

    .edit-todo-input {
        font-size: 1em;
        font-weight: 200;
        border: none;
        padding: 10px 30px;
        font-style: italic;
        background: #006989;
        color: #EAEBED;
        -webkit-appearance: none;
        outline: none;
        border-radius: 10px;
        cursor: pointer;
    }

    .strike {
        text-decoration: line-through;
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
