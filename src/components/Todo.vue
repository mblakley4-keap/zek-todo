<template>
    <div class="card">
        <div class="content" v-show="!editing">
            <input type="checkbox" class="circle" @click="completeTodo(todo)" v-model="todo.done" />
            <label @dblclick="editTodo">{{ todo.title }}</label>
            <button class="delete" @click="deleteTodo(todo)">X</button>
        </div>

        <div class="content" v-show="editing">
            <div></div>
            <input 
                type="text"
                v-model="editedTitle"
                class='edit-todo-input'
                @blur="editCancel()"
                @keyup.enter="editDone(todo)"
                @keyup.esc="editCancel()"
            />
            <label for="todo.title"></label>
        </div>

    </div>
</template>

<script>
export default {
    props: ["todo"],
    data () {
        return {
            editedTitle: "",
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
            this.editedTitle = this.todo.title;
            this.editing = true;
        },

        editDone(todo) {
            const value = this.editedTitle.trim();
            
            if (!value) {
                this.editedTitle = "";
                this.editing = false;
                return
            }

            todo.title = value;
            
            this.editedTitle = "";

            this.editing = false;
        },

        editCancel() {
            this.editedTitle = "";
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

    input {
        margin: 5px;
        padding: 5px;
        font-size: 16px;
    }

    label {
        display: block;
    }
</style>
