<template>
  <div>
    <ul>
      <li v-for="(single_news, index) in news" :key="index">
        {{ single_news.title }}<br>
        {{ single_news.published }}<br>
        {{ single_news.content }}<br>
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
      axios.get('http://localhost:3000/news')
        .then(res => (this.news = res.data))
    },
  },
  mounted () {
    this.fetchData()
  }
}
</script>
