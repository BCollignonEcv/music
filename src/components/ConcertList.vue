<template>
  <div>
      <div v-show="concerts_incoming.length > 0">
        <h2>Concerts à venir</h2>
        <div id="concertList" class="flex flex-item">
          <div class="card-item" v-for="(concert, index) in concerts_incoming" :key="index">
            <h4 class="card-title">{{concert.name}}</h4>
            <hr>
            <p>Date : {{ concert.date }}</p>
          </div>
        </div>
      </div>
      <hr>
      <div v-show="concerts_pasted.length > 0">
        <h2>Concerts passés</h2>
        <div id="concertList" class="flex flex-item">
          <div class="card-item" v-for="(concert, index) in concerts_pasted" :key="index">
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
  data () {
    return {
      concerts_incoming: [],
      concerts_pasted: [],
    }
  },
  methods: {
    async fetchData () {
      var currentDate = new Date(Date.now()).toLocaleString().split(',')[0]
      axios.get('http://localhost:3000/concerts?artistId=' + this.$route.params.id + '_sort=date&_order=desc&date<=' + currentDate)
        .then(res => (this.concerts_incoming = res.data))
      axios.get('http://localhost:3000/concerts?artistId=' + this.$route.params.id)
        .then(res => (this.concerts_pasted = res.data))
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
