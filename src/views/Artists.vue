<template>
<div>
  <header-app/>
  <artist-list/>
</div>
</template>

<style>

.artist .title{
    text-align: center;
}

</style>

<script>
import Header from '@/components/Header'
import axios from 'axios'
import ArtistList from '../components/ArtistList.vue'

export default {
  components: {
    'header-app': Header,
    'artist-list': ArtistList,
  },
  props: ['limit'],
  data () {
    return {
      artists: [],
      numberLimit: this.limit,
    }
  },
  methods: {
    async fetchData () {
      var url = 'http://localhost:3000/artists?_sort=date'
      if (this.numberLimit) {
        url = url + '&_limit=' + this.numberLimit
      }
      console.log(url)
      axios.get(url)
        .then(res => (this.artists = res.data))
    },
  },
  mounted () {
    this.fetchData()
  }
}
</script>
