<template>
  <div v-show="albums.length > 0">
    <h2> Tous les albums </h2>
    <div id="albumList" class="flex flex-item">
      <div class="card-item" v-for="(album, index) in albums" :key="index">
        <h4 class="card-title">{{album.name}}</h4>
        <hr>
        <p>Date de sortie : {{ album.released }}</p>
        <p>Nombre de tracks : {{ album.tracks }}</p>
      </div>
    </div>
    <hr>
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
      if (this.$route.params.id) {
        axios.get('http://localhost:3000/albums?artistId=' + this.$route.params.id)
          .then(res => (this.albums = res.data))
      } else {
        axios.get('http://localhost:3000/albums')
          .then(res => (this.albums = res.data))
      }
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
