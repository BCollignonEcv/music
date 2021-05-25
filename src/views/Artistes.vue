<template>
  <div>
    <h1> Artiste </h1>
    <label>Nom du groupe ou de l'artiste</label>
    <input v-model="groupename"/>
    <label>Photo de profil</label>
    <input v-model="profilpicture"/>
    <label>Genres</label>
    <select v-model="selectCountry">
      <option disabled value="">Choisissez</option>
      <option v-for="country in countries" :key="country.alpha2Code">
        {{ country.name }}
      </option>
    </select>
    <label>Pays</label>
    <select v-model="selectGenre">
      <option disabled value="">Choisissez</option>
      <option v-for="genre in genres" :key="genre.id">
        {{ genre.name }}
      </option>
    </select>
    <label>Description de l'artiste</label>
    <textarea v-model="description"></textarea>
    <button @click="submitForm">S'inscrire</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      groupename: null,
      profilpicture: null,
      selectGenre: '',
      selectCountry: '',
      countries: [],
      genres: [],
    }
  },
  methods: {
    async submitForm () {
      const res = await axios.post('http://localhost:3000/artistes', {
        userid: localStorage.getItem('vuejs_user_id'),
        groupename: this.groupename,
        avatar: this.profilpicture,
        genre: this.selected,
        like: 0,
      })
      console.log('submit : ' + res)
    },
  },
  mounted () {
    axios.get('https://restcountries.eu/rest/v2/all')
      .then(res => (this.countries = res.data))

    const token = localStorage.getItem('vuejs_token')
    axios.get('http://localhost:3000/genres', 
      { headers: { Authorization: `Bearer ${token}` } }
    ).then(res => (this.genres = res.data))
  }
}
</script>
