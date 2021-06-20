<template>
  <div>
    <div class="container">
    <h1> Album </h1>
    <label>Nom de l'album</label>
    <input v-model="name" required/>
    <label>Date de sortie</label>
    <input v-model="released" type="date" required/>
    <label>Nombre de tracks</label>
    <input v-model="tracks" type="number" required/>
    <label>Artiste</label>
    <select v-model="artistId" required>
      <option disabled value="">Choisissez</option>
      <option v-for="(artist, index) in artists" :key="index" :value="artist.id">
        {{ artist.name }}
      </option>
    </select>
    <button @click="submitForm">Enregister l'album</button>
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
      released: '',
      tracks: '',
      artistId: '',
      artists: [],
    }
  },
  methods: {
    async submitForm () {
      await axios.post('http://localhost:3000/albums', {
        userid: localStorage.getItem('vuejs_user_id'),
        name: this.name,
        released: this.released,
        tracks: this.tracks,
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
