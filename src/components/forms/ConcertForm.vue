<template>
  <div>
    <div class="container">
    <h1> Concert</h1>
    <label>Nom du concert</label>
    <input v-model="name" required/>
    <label>Date</label>
    <input v-model="date" type="date" required/>
    <label>Artiste</label>
    <select v-model="artistId" required>
      <option disabled value="">Choisissez</option>
      <option v-for="(artist, index) in artists" :key="index" :value="artist.id">
        {{ artist.name }}
      </option>
    </select>
    <button @click="submitForm">Enregister le concert</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import router from '@/router'

export default {
  data () {
    return {
      name: '',
      date: '',
      artistId: '',
      artists: [],
    }
  },
  methods: {
    async submitForm () {
      await axios.post('http://localhost:3000/concerts', {
        userid: localStorage.getItem('vuejs_user_id'),
        name: this.name,
        date: this.date,
        artistId: this.artistId,
      }).then(res => {
        if (!res.data.error) {
          router.push('/artist/' + this.artistId)
        }
      })
    },
    async setupForm () {
      axios.get('http://localhost:3000/artists')
        .then(res => (this.artists = res.data))
    }
  },
  beforeMount () {
    this.setupForm()
  }
}
</script>
