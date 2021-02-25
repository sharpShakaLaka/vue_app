<template>
	<base-dialog @closeDialog="confirmError" v-if="inputIsInvalid" title="Error!">
		<template #default>
			<p>Some fields are empty! Please, enter at least some characters into each field!</p>
		</template>
		<template #actions>
			<base-button @click="confirmError">Close</base-button>
		</template>
	</base-dialog>
  <base-card>
    <form @submit.prevent="submitData" action="">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="desrc">Description</label>
        <textarea id="descr" name="descr" rows="3" ref="descrInput" />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="text" id="link" name="link" ref="linkInput" />
      </div>
      <base-button type="submit">Add Resource</base-button>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
			inputIsInvalid: false
		};
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescr = this.$refs.descrInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescr.trim() === '' ||
        enteredLink.trim() === ''
      ) {
				this.inputIsInvalid = true;
				return;
			}
        this.addResource(enteredTitle, enteredDescr, enteredLink);
				this.$refs.titleInput.value = '';
				this.$refs.descrInput.value = '';
				this.$refs.linkInput.value = '';
    },
		confirmError() {
			this.inputIsInvalid = false;
		}
  }
};
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
