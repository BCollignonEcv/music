<template>
  <div>
    <ul>
      <li v-for="(artist, index) in artists" :key="index">
        {{ artist.name }}<br>
        {{ artist.country }}<br>
        {{ artist.genreId }}<br>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      artists: [],
    }
  },
  methods: {
    async fetchData () {
      const token = localStorage.getItem('vuejs_token')

      const res = axios.get('http://localhost:3000/artists', {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
        .then(function (res) {
          if (res.statusText === 'OK') {
            console.info(res.data)
            this.artists = res.data
          }
        })
        .catch(function (error) {
          console.log(error)
          console.log(res)
        })
    }
  },
  created () {
    this.fetchData()
  }
}
</script>
