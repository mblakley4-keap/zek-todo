<template>
    <div class="card">
        <div class="content" v-show="!isEditing">
            <div class="header">
                {{ todo.title }}
            </div>

            <div class="meta">
                {{ todo.project }}
            </div>

            <div class="extra-content">
                <span class="edit-icon clickable" v-on:click="showForm">
                    ⚙️
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
                    <label for="todo.project">Project</label>
                    <input type="text" v-model="todo.project">
                </div>

                <div class="close">
                    <button class="clickable" v-on:click="hideForm">
                        Close
                    </button>
                </div>
            </div>

        </div>


        <div class="status" v-show="todo.done">
            🟢 Complete
        </div>

        <div class="status" v-show="!todo.done">
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
    },
};
</script>

<style>
.card {
    margin: 10px auto;
    padding: 5px;
    border: 1px solid green;
    width: 25%;
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
