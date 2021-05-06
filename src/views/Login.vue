<template>
  <div>
  <header-app/>
    <div class="container">
     <div class="row">
     <div class="col"></div>
     <div class="col-12 col-lg-5">
      <h1 class="my-5"> Se connecter </h1>
    <form>
    <div class="form-group mb-3">
      <label>Adresse mail</label>
      <input type="email" class="form-control"  placeholder="Enter email" v-model="email"/>
    </div>
    <div class="form-group">
      <label>Mot de Passe</label>
      <input type="password" class="form-control" placeholder="Mot de passe" v-model="password"/>
    </div>
      <button type="submit" class="btn btn-primary my-2" @click="submitLogin">Connexion</button>
    </form>
      </div>
      <div class="col"></div>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import jwt_decode from "jwt-decode"
import Header from '@/components/Header'

export default {
  components: {
    'header-app': Header,
  },
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
      const { accessToken } = res.data

      const { sub } = jwt_decode(accessToken)

      localStorage.setItem('vuejs_token', accessToken)
      localStorage.setItem('vuejs_user_id', sub)
    }
  }
}
</script>
