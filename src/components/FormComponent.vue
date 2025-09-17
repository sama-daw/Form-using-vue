<template>
  <form @submit.prevent="onSubmit" class="form-container">
    <div class="form-group">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="name" @blur="validateField('name')" />
      <span v-if="errors.name" class="error">{{ errors.name }}</span>
    </div>

    <div class="form-group">
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="email" @blur="validateField('email')" />
      <span v-if="errors.email" class="error">{{ errors.email }}</span>
    </div>

    <div class="form-group">
      <label for="phone">Phone:</label>
      <input type="text" id="phone" v-model="phone" @blur="validateField('phone')" />
      <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
    </div>

    <div class="form-group">
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="password" @blur="validateField('password')" />
      <span v-if="errors.password" class="error">{{ errors.password }}</span>
    </div>

    <div class="form-group">
      <label for="confirmPassword">Confirm Password:</label>
      <input type="password" id="confirmPassword" v-model="confirmPassword" @blur="validateField('confirmPassword')" />
      <span v-if="errors.confirmPassword" class="error">{{ errors.confirmPassword }}</span>
    </div>

    <div class="form-group">
      <label for="country">Country:</label>
      <select id="country" v-model="country" @blur="validateField('country')">
        <option disabled value="">Please select one</option>
        <option>USA</option>
        <option>Canada</option>
        <option>UK</option>
        <option>Australia</option>
      </select>
      <span v-if="errors.country" class="error">{{ errors.country }}</span>
    </div>

    <div class="form-group">
      <label for="message">Suggestions:</label>
      <textarea id="message" v-model="message" @blur="validateField('message')" rows="4" placeholder="Your suggestions..."></textarea>
      <span v-if="errors.message" class="error">{{ errors.message }}</span>
    </div>

    <div class="form-group checkbox-group">
      <input type="checkbox" id="agree" v-model="agree" @change="validateField('agree')" />
      <label for="agree">I agree to the terms and conditions</label>
      <span v-if="errors.agree" class="error">{{ errors.agree }}</span>
    </div>

    <button type="submit" class="submit-btn">Submit</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
      phone: '',
      password: '',
      confirmPassword: '',
      country: '',
      message: '',
      agree: false,
      errors: {
        name: '',
        email: '',
        phone: '',
        password: '',
        confirmPassword: '',
        country: '',
        message: '',
        agree: '',
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
      } else if (field === 'phone') {
        const phonePattern = /^[0-9]{10,15}$/;
        this.errors.phone = phonePattern.test(this.phone) ? '' : 'Phone must be 10-15 digits.';
      } else if (field === 'password') {
        this.errors.password = this.password.length >= 6 ? '' : 'Password must be at least 6 characters.';
      } else if (field === 'confirmPassword') {
        this.errors.confirmPassword = this.confirmPassword === this.password ? '' : 'Passwords do not match.';
      } else if (field === 'country') {
        this.errors.country = this.country ? '' : 'Country is required.';
      } else if (field === 'message') {
        this.errors.message = this.message.trim() ? '' : 'Please enter your suggestions.';
      } else if (field === 'agree') {
        this.errors.agree = this.agree ? '' : 'You must agree to the terms.';
      }
    },
    onSubmit() {
      [
        'name', 'email', 'phone', 'password', 'confirmPassword',
        'country', 'message', 'agree'
      ].forEach(field => this.validateField(field));


      if (
        !this.errors.name &&
        !this.errors.email &&
        !this.errors.phone &&
        !this.errors.password &&
        !this.errors.confirmPassword &&
        !this.errors.country &&
        !this.errors.message &&
        !this.errors.agree
      ) {
        alert('Form submitted successfully!');
      }
    },
  },
};
</script>

<style scoped>
.form-container {
  max-width: 450px;
  margin: 30px auto;
  padding: 30px 35px;
  border-radius: 12px;
  background: #181818;
  box-shadow: 0 6px 18px rgba(212, 175, 55, 0.35);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #fdf6e3;
  border: 1.5px solid #af9500;
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
}

label {
  font-weight: 700;
  font-size: 1.14rem;
  margin-bottom: 8px;
  color: #ffe082;
  text-shadow: none;
}

input, select, textarea {
  padding: 14px 18px;
  font-size: 1rem;
  border: 2px solid #af9500;
  border-radius: 10px;
  background-color: #232323;
  color: #fffde7;
  box-shadow: none;
  font-weight: 500;
  transition: border-color 0.3s, background 0.3s, color 0.3s;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

input::placeholder,
textarea::placeholder {
  color: #bca968cc;
}

input:focus,
select:focus,
textarea:focus {
  border-color: #ffe082;
  background-color: #181818;
  color: #fffde7;
  outline: none;
}

.error {
  color: #ff6565;
  margin-top: 6px;
  font-size: 0.95rem;
  font-weight: 600;
  text-shadow: none;
}

.checkbox-group {
  flex-direction: row;
  align-items: center;
}

.checkbox-group label {
  margin-left: 8px;
  font-weight: 500;
  color: #ffe082;
}

.submit-btn {
  background: linear-gradient(135deg, #ffd700 0%, #af9500 100%);
  color: #181818;
  font-weight: 700;
  padding: 16px 0;
  border: none;
  border-radius: 14px;
  cursor: pointer;
  width: 100%;
  font-size: 1.13rem;
  letter-spacing: 1.3px;
  box-shadow: 0 5px 16px rgba(212, 175, 55, 0.35);
  text-shadow: none;
  transition: background 0.3s, box-shadow 0.3s;
}

.submit-btn:hover {
  background: linear-gradient(135deg, #fff8d1 10%, #ffd700 100%);
}
</style>
