
<template>
  <div id="sign-in" class="container">
    <main>
      <section class="hero">
        <h1>SIGN IN TO YOUR ACCOUNT</h1>
        <p>Enter your credentials to access your account and manage your listings.</p>
        <form @submit.prevent="loginUser">
          <div class="form-group">
            <label>Email</label>
            <input v-model="user.email" class="form-control" type="email" placeholder="Email" />
          </div>
          <div class="form-group">
            <label>Password</label>
            <input v-model="user.password" class="form-control" type="password" placeholder="Password" />
          </div>
          <button type="submit" class="btn btn-primary">Login</button>
        </form>
        <div class="mt-3">
          <span>Not registered? <router-link to="/register">Register/SignUp Here</router-link></span>
        </div>
      </section>
    </main>
  </div>
</template>

<script>

import axios from "axios";
import AuthService from '@/service/AuthService';

export default {
  data() {
    return {
      user: {
        email: '',
        password: ''
      }
    };
  },
  methods: {
    async loginUser() {
      try {
        const response = await axios.post('http://localhost:8080/auth/login', {
          email: this.email,
          password: this.password,
        });

        const token = response.data.token;
        localStorage.setItem('authToken', token);

      } catch (error) {
        this.errorMessage = 'Error registering account. Please try again.';
      }
      this.$router.push({name: 'SellerFunction'});
    }
  }
  };

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Roboto:wght@400;500;700&display=swap');

:root {
  --primary-color: #8c7851;
  --secondary-color: #d4c6a9;
  --text-color: #333;
  --background-color: #f8f4ef;
  --light-gray: #f0f0f0;
  --font-heading: 'Playfair Display', serif;
  --font-body: 'Roboto', sans-serif;
}

body {
  margin: 0;
  font-family: var(--font-body)serif;
  color: var(--text-color);
  background-color: var(--light-gray);
}

.hero {
  padding: 4rem 2rem;
  text-align: center;
  background-color: var(--background-color);
  border-radius: 8px;
}

h1 {
  font-family: var(--font-heading),serif;
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

.login-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-group {
  margin-bottom: 1rem;
  width: 100%;
  max-width: 400px;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
}

.form-group input {
  width: 100%;
  padding: 0.8rem;
  border: 1px solid var(--secondary-color);
  border-radius: 4px;
  font-size: 1rem;
}

button {
  background-color: var(--secondary-color);
  border: none;
  color: var(--text-color);
  padding: 0.8rem 1.5rem;
  text-align: center;
  font-size: 1rem;
  border-radius: 4px;
  cursor: pointer;
}
</style>
