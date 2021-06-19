<template>
  <div>
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
      const token = localStorage.getItem('vuejs_token')

      const res = axios.get('http://localhost:3000/concerts', {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
      console.log(res)
      this.concerts = res.data
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
