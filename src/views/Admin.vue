<template>
  <div>
    <header-app/>
    <div class="flex justify-between">
        <button @click='showArtisteFrom = !showArtisteFrom'>Ajouter un artiste</button>
        <button @click='showConcertFrom = !showConcertFrom'>Ajouter un concert</button>
        <button @click='showAlbumFrom = !showAlbumFrom'>Ajouter un album</button>
        <button @click='showNewsFrom = !showNewsFrom'>Ajouter une news</button>
    </div>
    <div>
        <artist-form v-if="showArtisteFrom"/>
        <concert-form v-if="showConcertFrom"/>
        <album-form v-if="showAlbumFrom"/>
        <news-form v-if="showNewsFrom"/>
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header'
import ArtistForm from '../components/forms/ArtistForm'
import ConcertForm from '../components/forms/ConcertForm'
import AlbumForm from '../components/forms/AlbumForm'
import NewsForm from '../components/forms/NewsForm'

export default {
  components: {
    'header-app': Header,
    'artist-form': ArtistForm,
    'concert-form': ConcertForm,
    'album-form': AlbumForm,
    'news-form': NewsForm,
  },
  data () {
    return {
      showArtisteFrom: true,
      showConcertFrom: false,
      showAlbumFrom: false,
      showNewsFrom: false,
    }
  },
  methods: {

  }
}
</script>
