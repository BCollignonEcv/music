<template>
<div>
  <header-app/>
  <div class="container pt-5">
    <div class="flex">
        <div v-for="(artist, index) in artists" :key="index">
            <div class="artist-picture mb-4 mx-3" v-bind:style="{ 'background-image': 'url(' + artist.avatar + ')' }"></div>
            <h3>{{artist.name}}</h3>
        </div>
    </div>
  </div>
</div>
</template>

<script>
import Header from '@/components/Header'
import axios from 'axios'

export default {
  components: {
    'header-app': Header,
  },
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
