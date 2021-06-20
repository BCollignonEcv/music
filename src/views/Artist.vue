<template>
  <div>
    <header-app/>
    <div class="container pt-5">
      <div class="row">
        <div class="artist-picture mb-4 mx-3" v-bind:style="{ 'background-image': 'url(' + artist.avatar + ')' }"></div>
        <h1>{{artist.name}}</h1>
        <h3>Genre : {{artist.genreId}}</h3>
        <h3>Pays : {{artist.country}}</h3>
        <h3>Like : {{artist.likes}}</h3>

        <a data-toggle="collapse" href="#collapseDescritpion" role="button" aria-expanded="false" aria-controls="collapseDescritpion">
          Voir la description
        </a>
        <div class="collapse" id="collapseDescritpion">
          <div class="card card-body">
            <p>{{artist.description}}</p>
          </div>
        </div>

        <concert-list />
        <album-list />
      </div>
    </div>
  </div>
</template>

<style>
  .artist-picture {
    height: 150px;
    width: 150px;
    background-size: cover;
    border-radius: 50%;
  }
  #collapseDescritpion .card{
    background: none;
    border: none;
  }

  .card-item{
    padding: 12px;
    min-height: 60px;
    width: 200px;
    border: 1px solid #FF5F1F;
    border-radius: 12px;
    background-color: #333333;
  }

  .card-item.card-title{
    color: #FF5F1F;
  }
</style>

<script>
import Header from '@/components/Header'
import axios from 'axios'
import ConcertList from '@/components/ConcertList'
import AlbumList from '../components/AlbumList.vue'

export default {
  components: {
    'header-app': Header,
    'concert-list': ConcertList,
    'album-list': AlbumList,
  },
  data () {
    return {
      artist: [],
    }
  },
  methods: {
    async fetchData () {
      axios.get('http://localhost:3000/artists/' + this.$route.params.id)
        .then(res => (this.artist = res.data))
    },
  },
  mounted () {
    this.fetchData()
  }
}
</script>
