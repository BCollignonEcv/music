<template>
  <div>
    <div class="container">
    <h1>News</h1>
    <label>Titre</label>
    <input v-model="title" required/>
    <label>Contenu</label>
    <textarea v-model="content" required></textarea>
    <button @click="submitForm">Enregister la news</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import router from '@/router'

export default {
  data () {
    return {
      title: '',
      content: '',
      published: new Date(Date.now()).toLocaleString().split(',')[0],
    }
  },
  methods: {
    async submitForm () {
      await axios.post('http://localhost:3000/news', {
        userid: localStorage.getItem('vuejs_user_id'),
        title: this.title,
        published: this.published,
        content: this.content,
      }).then(res => {
        if (!res.data.error) {
          router.push('/news')
        } else {
          console.log(res)
        }
      })
    },
  },
}
</script>
