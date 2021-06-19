<template>
  <div>
    <h2> Tous les albums </h2>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      albums: [],
    }
  },
  methods: {
    async fetchData () {
      const token = localStorage.getItem('vuejs_token')

      const res = axios.get('http://localhost:3000/albums', {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
      console.log(res)
      this.albums = res.data
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
