<template>
  <div>
    <h1> Login </h1>
    <label>Login</label>
    <input v-model="email"/>
    <label>Password</label>
    <input type="password" v-model="password"/>
    <button @click="submitLogin">Connexion</button>
    <button @click="register">S'inscrire</button>
  </div>
</template>

<script>
import axios from 'axios'
import jwt_decode from "jwt-decode"
import router from '@/router'
export default {
  data () {
    return {
      email: null,
      password: null,
    }
  },
  methods: {
    async submitLogin () {
      const res = await axios.post('http://localhost:3000/login', {
        email: this.email,
        password: this.password,
      })
      
      if (res) {
        const { accessToken } = res.data

        const { sub } = jwt_decode(accessToken)

        localStorage.setItem('vuejs_token', accessToken)
        localStorage.setItem('vuejs_user_id', sub)

        router.push('/')
      }
    },

    register () {
      router.push('/register')
    }
  }
}
</script>
