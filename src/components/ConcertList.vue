<template>
  <div>
    <li v-for="(concert, index) in concerts" :key="index">
      {{ concert.name }}<br>
      {{ concert.date }}<br>
      {{ concert.artistId }}<br>
    </li>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      concerts: [],
    }
  },
  methods: {
    async fetchData () {
      axios.get('http://localhost:3000/concerts')
        .then(res => (this.concerts = res.data))
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
