<template>
  <div class="container pt-5">
    <h2>Artistes</h2>
    <div class="flex">
      <div class="artist" v-for="(artist, index) in artists" :key="index">
          <a v-bind:href="'/artist/' + artist.id" >
            <div class="artist-picture mb-4 mx-3" v-bind:style="[artist.avatar ? { 'background-image': 'url(' + artist.avatar + ')' } : { 'background-image': 'url(\'https://i1.sndcdn.com/avatars-000196113278-93p2dw-t500x500.jpg\')'}]" ></div>
            <h3 class="title">{{artist.name}}</h3>
          </a>
      </div>
    </div>
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
