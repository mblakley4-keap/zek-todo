<template>
  <div class='create-form-container'>
      <button @click='openForm' v-show='!isCreating'>
          <i>Add Todo</i>
      </button>
      <div class='card' v-show='isCreating'>
          <div class='content'>
              <div class='form'>
                  <div class='field'>
                      <label for='title'>Title</label>
                      <input id='title' type="text" v-model='newTitle' ref='title' defaultValue=''>
                  </div>

                  <div class='field'>
                      <label for='description'>Description</label>
                      <input id='description' type="text" v-model='newDescription' ref='description' defaultValue=''>
                  </div>

                  <div class='button-container'>
                      <button @click='sendForm()'>
                          Create
                      </button>
                     
                      <button @click='closeForm()'>
                          Cancel
                      </button>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            newTitle: '',
            newDescription: '',
            isCreating: false,
        };
    },

    methods: {
        openForm() {
            this.isCreating = true;
        },

        closeForm() {
            this.isCreating = false;
        },

        sendForm() {
            if (this.newTitle.length > 0) {
                const title = this.newTitle;

                const description = this.newDescription;

                this.$emit('add-todo', {
                    title,
                    description,
                });
                this.isCreating = false;
                this.newTitle = '';
                this.newDescription = '';
            } else alert('Please add a title')
        },
    },
};
</script>

<style>

</style>