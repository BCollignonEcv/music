<template>
  <div>
  <header-app/>
    <div class="container login-form">
      <div class="row h-100">
        <div class="col-4"></div>
        <div class="col-12 col-lg-4 login">
            <logo-neon/>
            <form>
              <h1 class="mb-5"> Se connecter </h1>
              <NeonTitle/>
              <div class="form-group mb-3">
                <label>Adresse mail</label>
                <input type="email" class="form-control"  placeholder="Enter email" v-model="email"/>
                </div>
              <div class="form-group">
                <label>Mot de Passe</label>
                <input type="password" class="form-control" placeholder="Mot de passe" v-model="password"/>
              </div>
            <button type="submit" class="btn btn-primary my-3" @click="submitLogin">Connexion</button>
            <p class="text-center mt-4 text-secondary">Vous n'avez pas encore de compte ? <a @click="register">Créer un compte</a></p>
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
import LogoNeon from '@/components/LogoNeon'

export default {
  components: {
    'header-app': Header,
    'logo-neon': LogoNeon,
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
