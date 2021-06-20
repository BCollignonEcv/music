<template>
  <div>
    <div class="news" v-for="(single_news, index) in news" :key="index">
      <div class="flex justify-between">
        <h3>{{ single_news.title }}</h3>
        <p>{{ single_news.published }}</p>
      </div>
      <hr>
      {{ single_news.content }}<br>
    </div>
  </div>
</template>

<style>
  .news{
    margin-top: 24px;
  }
</style>

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
