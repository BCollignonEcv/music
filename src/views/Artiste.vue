<template>
<div>
  <header-app/>
  <div class="container pt-5">
    <div class="row">
      <div class="artist-picture mb-4 mx-3"></div>
      <h1>Nom de l'artiste</h1>
      <h2>Genre : </h2>
      <a data-toggle="collapse" href="#collapseDescritpion" role="button" aria-expanded="false" aria-controls="collapseDescritpion">
        En savoir plus
      </a>
      <div class="collapse" id="collapseDescritpion">
        <div class="card card-body">
          Description...
        </div>
      </div>
      
      <h2>Concerts</h2>
       <ul>
        <li v-for="(concert, artistId) in concerts" :key="artistId">
          {{ concert.name }}<br>
          {{ concert.released }}<br>
          {{ concert.tracks }}<br>
        </li>
      </ul>
      <hr>
      <h2>Albums</h2>
      <hr>
      <ul>
        <li v-for="(album, artistId) in albums" :key="artistId">
          {{ album.name }}<br>
          {{ album.released }}<br>
          {{ album.tracks }}<br>
        </li>
      </ul>
    </div>
  </div>
</div>
</template>

<style>
  .artist-picture {
    height: 150px;
    width: 150px;
    background: url("https://upload.wikimedia.org/wikipedia/commons/thumb/d/de/Festival_des_Vieilles_Charrues_2018_-_Damso_-_006.jpg/800px-Festival_des_Vieilles_Charrues_2018_-_Damso_-_006.jpg");
    background-size: cover;
    border-radius: 50%;
  }
  #collapseDescritpion .card{
    background: none;
    border: none;
  }
</style>

<script>
import Header from '@/components/Header'
import axios from 'axios'
export default {
  components: {
    'header-app': Header,
  },
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
