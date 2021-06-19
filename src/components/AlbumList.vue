<template>
  <div>
    <h2> Tous les albums </h2>
    <li v-for="(album, index) in albums" :key="index">
      {{ album.name }}<br>
      {{ album.released }}<br>
      {{ album.tracks }}<br>
      {{ album.artistId }}<br>
    </li>
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
      axios.get('http://localhost:3000/albums')
        .then(res => (this.albums = res.data))
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
