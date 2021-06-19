<template>
  <div>
    <ul>
      <li v-for="news_single in news" :key="news_single.title">
        {{ news_single.title }}<br>
        {{ news_single.content }}<br>
        {{ news_single.published }}<br>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      news: [],
    }
  },
  methods: {
    async fetchData () {
      const token = localStorage.getItem('vuejs_token')

      const res = axios.get('http://localhost:3000/news', {
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
      console.log(res)
      this.news = res.data
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>
