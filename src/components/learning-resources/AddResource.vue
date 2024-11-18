<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      title: '',
      description: '',
      url: '',
      isInvalidForm: false,
    }
  },
  computed: {
    isFormValid() {
      return this.title !== '' && this.description !== '' && this.url !== ''
    },
  },
  methods: {
    submitData() {
      if (!this.isFormValid) {
        this.isInvalidForm = true
        return
      }
      this.addResource(this.title, this.description, this.url)
    },
    confirmError() {
      this.isInvalidForm = false
    },
  },
}
</script>

<template>
  <base-dialog v-if="isInvalidForm" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>One input value is invalid.</p>
      <p>Please check all input again</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Ok</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" v-model="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" v-model="description"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" v-model="url" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
