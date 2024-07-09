<template>
  <div class="login-container">
    <div class="login-form">
      <q-input label="E-mail" v-model="email" class="login-input" />
      <q-input label="Senha" type="password" v-model="password" class="login-input" />
      <q-btn type="positive" label="Login" @click="entrar" class="login-button" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { api } from 'boot/axios'
import { useRouter } from 'vue-router'

const router = useRouter()

const email = ref('')
const password = ref('')

const entrar = async () => {
  const res = await api.post('/auth/login', {
    email: email.value,
    password: password.value
  })
  localStorage.setItem('token', res.data.token)
  router.push('/')
}
</script>

<style>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f5f5f5;
}

.login-form {
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

.login-input {
  margin-bottom: 20px;
}

.login-button {
  align-self: center;
}
</style>
