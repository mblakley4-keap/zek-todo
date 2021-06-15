<template>
    <input 
        type='text'
        autofocus
        v-model='newTodo'
        class='create-todo-input'
        placeholder='Make a todo'
        @keyup.enter='addTodo'
    />
</template>

<script>
export default {
    data() {
        return {
            newTodo: "",
        };
    },

    methods: {
        addTodo() {
            const value = this.newTodo.trim();

            if (!value) return;
            
            this.$emit('add-todo');
            this.newTodo = "";
        }
    },
};
</script>

<style>
    .create-todo-input {
        width: 80%;
        padding: 15px 30px;
        font-size: 2em;
        border: none;
        color: #EAEBED;
        background: #006989;
        box-shadow: 1px 1px 5px 1px #A3BAC3;
        border-radius: 10px;
    }

    input:focus {
        outline: none;
    }

    ::placeholder {
        color: #A3BAC3;
    }

</style>