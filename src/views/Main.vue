<template>
  <div>
   <header-app/>
   <div class="container">
    <div class="row">
      <artist-list limit="10"/>
      <concert-list limit="10"/>
      <album-list limit="10"/>
    </div>
  </div>

  </div>
</template>

<script>
import ConcertList from '@/components/ConcertList'
import AlbumList from '@/components/AlbumList'
import ArtistList from '@/components/ArtistList'
import Header from '@/components/Header'

export default {
  components: {
    'concert-list': ConcertList,
    'album-list': AlbumList,
    'artist-list': ArtistList,
    'header-app': Header,
  }
}
</script>
