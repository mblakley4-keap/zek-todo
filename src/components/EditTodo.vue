<template>
    <div>
        <input 
            type="text"
            ref="title"
            v-model="editedTitle"
            class='edit-todo-input'
            @blur="editCancel()"
            @keyup.enter="editDone()"
            @keyup.esc="editCancel()"
        />
        <label for="todo.title"></label>
    </div>
</template>

<script>

export default {
    mounted() {
        this.focusInput();
    },

    props: ["todo"],

    data() {
        return {
            editedTitle: this.todo.title,
        }
    },

    methods: {
        focusInput() {
            this.$refs.title.focus();
        },

        editDone() {
            this.$emit('edit-done', this.editedTitle);
            this.editedTitle = "";
        },

        editCancel() {
            this.$emit('edit-cancel');
            this.editedTitle = "";
        }
    }
}
</script>

<style>

</style>