<style>
  :root {
    --header-height:80px;
  }
  nav {
    padding: 16px 24px;
    background: #262626;
    font-size: 24px;
    color: white;
    box-shadow: 0px 3px 3px #303030;
    letter-spacing: 1px;
  }
  .header-app {
    height: var(--header-height);
  }
</style>

<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-dark header-app">
    <a class="navbar-brand" href="/">LastMusic</a>
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item">
        <a class="nav-link" href="/artists">Artistes</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="/news" >News</a>
      </li>
    </ul>
  </div>
   <a v-if="logged" class="nav-link login-nav-link" href="/admin">Admin</a>
   <a v-else class="nav-link login-nav-link" href="/login">Login/Register</a>
    </nav>
  </header>
</template>

<script>
import auth from '@/api/auth'

export default {
  data () {
    return {
      logged: false,
    }
  },
  methods: {
    checkLoggedIn () {
      try {
        auth.get(`/users/${localStorage.getItem('vuejs_user_id')}`)
        this.logged = true
      } catch (e) {
        this.logged = false
      }
    }
  },
  beforeMount () {
    this.checkLoggedIn()
  }
}
</script>

