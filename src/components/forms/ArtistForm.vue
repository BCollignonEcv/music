<template>
  <div>
    <div class="container">
    <h1> Artiste</h1>
    <label>Nom du groupe ou de l'artiste</label>
    <input v-model="name" required/>
    <label>Photo de profil</label>
    <input v-model="profilpicture" type="url" required/>
    <label>Genres</label>
    <select v-model="selectGenre" required>
      <option disabled value="">Choisissez</option>
      <option v-for="genre in genres" :key="genre.id">
        {{ genre.name }}
      </option>
    </select>
    <label>Pays</label>
    <select v-model="selectCountry" required>
      <option disabled value="">Choisissez</option>
      <option v-for="country in countries" :key="country.alpha2Code">
        {{ country.name }}
      </option>
    </select>
    <label>Description de l'artiste</label>
    <textarea v-model="description" required></textarea>
    <button @click="submitForm">Enregister l'artiste</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import router from '@/router'

export default {
  data () {
    return {
      name: null,
      profilpicture: null,
      selectGenre: '',
      selectCountry: '',
      description: '',
      countries: [],
      genres: [],
    }
  },
  methods: {
    async submitForm () {
      await axios.post('http://localhost:3000/artists', {
        userid: localStorage.getItem('vuejs_user_id'),
        name: this.name,
        origin: this.selectCountry,
        avatar: this.profilpicture,
        genre: this.selected,
        description: this.description,
        like: 0,
      }).then(res => {
        if (!res.data.error) {
          router.push('/artist/' + res.data.id)
        }
      })
    },
    async setupForm () {
      axios.get('https://restcountries.eu/rest/v2/all')
        .then(res => (this.countries = res.data))

      axios.get('http://localhost:3000/genres')
        .then(res => (this.genres = res.data))
    }
  },
  beforeMount () {
    this.setupForm()
  }
}
</script>
