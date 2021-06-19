<template>
  <div>
   <header-app/>
   <div class="container">
    <div class="row">
      <h1> Music at time </h1>
      <h2> Toutes les news </h2>
      <news-list />
      <h2> Tous les concerts </h2>
      <concert-list />
      <album-list />
      <h2> Tous les artistes </h2>
      <artist-list />
    </div>
  </div>

  </div>
</template>

<script>
import NewsList from '@/components/NewsList'
import ConcertList from '@/components/ConcertList'
import AlbumList from '@/components/AlbumList'
import ArtistList from '@/components/ArtistList'
import Header from '@/components/Header'

export default {
  components: {
    'news-list': NewsList,
    'concert-list': ConcertList,
    'album-list': AlbumList,
    'artist-list': ArtistList,
    'header-app': Header,
  }
}
</script>
