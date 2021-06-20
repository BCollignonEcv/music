<template>
  <div>
      <div v-show="concerts.length > 0">
        <h2>Concerts</h2>
        <div id="concertList" class="flex flex-item">
          <div class="card-item" v-for="(concert, index) in concerts" :key="index">
            <h4 class="card-title">{{concert.name}}</h4>
            <hr>
            <p>Date : {{ concert.date }}</p>
          </div>
        </div>
      </div>
      <hr>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['limit'],
  data () {
    return {
      concerts: [],
      numberLimit: this.limit,
    }
  },
  methods: {
    async fetchData () {
      var url = 'http://localhost:3000/concerts?_sort=date'
      if (this.$route.params.id) {
        url = url + '&artistId=' + this.$route.params.id
      }
      if (this.numberLimit) {
        url = url + '&_limit=' + this.numberLimit
      }
      axios.get(url)
        .then(res => (this.concerts = res.data))
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
