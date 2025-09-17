<template>
  <form @submit.prevent="onSubmit">
    <div>
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="name" @blur="validateField('name')" />
      <span v-if="errors.name" style="color: red;">{{ errors.name }}</span>
    </div>

    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="email" @blur="validateField('email')" />
      <span v-if="errors.email" style="color: red;">{{ errors.email }}</span>
    </div>

    <button type="submit">Submit</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
      errors: {
        name: '',
        email: '',
      },
    };
  },
  methods: {
    validateField(field) {
      if (field === 'name') {
        this.errors.name = this.name.trim() ? '' : 'Name is required.';
      } else if (field === 'email') {
        const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        this.errors.email = emailPattern.test(this.email) ? '' : 'Invalid email.';
      }
    },
    onSubmit() {
      this.validateField('name');
      this.validateField('email');

      if (!this.errors.name && !this.errors.email) {
        alert('Form submitted successfully!');
      }
    },
  },
};
</script>
