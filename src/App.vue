<template>
    <NavBar/>
    <router-view/>
</template>

<script>
import NavBar from '@/components/NavBar';

export default {
  name: 'App',
  components: {
    NavBar,
  },
  data: () => ({
    //
  }),
}
</script>

<style>
  body {
    background-color: #111;
    padding: 0 50px;
  }
</style>