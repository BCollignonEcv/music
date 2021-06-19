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
      axios.get('http://localhost:3000/artists')
        .then(res => (this.artists = res.data))
    },
  },
  mounted () {
    this.fetchData()
  }
}
</script>
