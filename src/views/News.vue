<template>
  <div>
    <header-app/>
    <div class="container pt-5">
        <news-list />
    </div>
  </div>
</template>

<style>

</style>

<script>
import Header from '@/components/Header'
import NewsList from '../components/NewsList.vue'

export default {
  components: {
    'header-app': Header,
    'news-list': NewsList,
  },
}
</script>
