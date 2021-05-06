<template>
  <div>
   <header-app/>
    <h1> Mon application </h1>
    <user-list />
  </div>
</template>

<script>
import UserList from '@/components/UserList'
import Header from '@/components/Header'

export default {
  components: {
    'user-list': UserList,
    'header-app': Header,
  }
}
</script>
