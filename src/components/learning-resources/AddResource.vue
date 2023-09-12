<template>
  <base-card>
    <form @submit.prevent="submit">
      <div class="form-control">
        <label for="title">Title</label>
        <input ref="titleInput" type="text" name="title" id="title">
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea ref="descriptionInput" rows="3" name="description" id="description"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input ref="linkInput" type="url" name="link" id="link">
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>

    </form>
  </base-card>
</template>
<script>
export default {
  emits: ['add-resource'],
  methods: {
    submit() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descriptionInput.value;
      const enteredLink = this.$refs.linkInput.value;
      this.$emit('add-resource', {
        title: enteredTitle,
        description: enteredDescription,
        link: enteredLink
      })
      console.log("Submitted");
    }
  }
}
</script>
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