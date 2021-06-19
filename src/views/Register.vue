<template>
  <div>
  <!--
    <h1> Inscription </h1>
    <label>Email</label>
    <input v-model="email"/>
    <label>Password</label>
    <input type="password" v-model="password"/>
    <label>Prénom</label>
    <input v-model="firstname"/>
    <label>Nom</label>
    <input v-model="lastname"/>
    <button @click="submitForm">S'inscrire</button>
    -->
  <header-app/>
     <div class="container register-form">
      <div class="row h-100">
        <div class="col-4"></div>
        <div class="col-12 col-lg-4 register">
            <form>
              <h1 class="mb-5">S'inscrire</h1>
              <NeonTitle/>
              <div class="form-group mb-3">
                <label>Adresse mail</label>
                <input type="email" class="form-control"  placeholder="Enter email" v-model="email"/>
              </div>
              <div class="form-group mb-3">
                <label>Mot de Passe</label>
                <input type="password" class="form-control" placeholder="Mot de passe" v-model="password"/>
              </div>
              <div class="form-group mb-3">
                <label>Prénom</label>
                <input type="firstname" class="form-control"  placeholder="Prénom" v-model="firstname"/>
              </div>
              <div class="form-group mb-3">
                <label>Nom</label>
                <input type="text" class="form-control"  placeholder="Nom" v-model="lastname"/>
              </div>
              <div class="form-group mb-3">
                <label>Nom du groupe</label>
                <input type="text" class="form-control"  placeholder="Prénom" v-model="groupename"/>
              </div>
            <button type="submit" class="btn btn-primary my-3" @click="submitForm">S'inscrire</button>
            <p class="text-center mt-4 text-secondary">Vous possédez déjà un compte ? <a href="/login">Se connecter</a></p>
          </form>
        </div>
        <div class="col-4"></div>
      </div>
    </div>
  </div>
  

 
   
  

</template>

<script>
import axios from 'axios'
import jwt_decode from "jwt-decode"
import router from '@/router'
import Header from '@/components/Header'

export default {
  components: {
    'header-app': Header,
  },
  data () {
    return {
      email: null,
      password: null,
      firstname: null,
      lastname: null,
    }
  },
  methods: {
    async submitForm () {
      const res = await axios.post('http://localhost:3000/register', {
        email: this.email,
        password: this.password,
        firstname: this.firstname,
        lastname: this.lastname,
      })

      if (res) {
        const { accessToken } = res.data

        const { sub } = jwt_decode(accessToken)

        localStorage.setItem('vuejs_token', accessToken)
        localStorage.setItem('vuejs_user_id', sub)

        router.push('/')
      }
    }
  }
}
</script>
