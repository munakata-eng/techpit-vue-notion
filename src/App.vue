<template>
  <div id="app">
    <NavigationBar />
    <MainPage />
  </div>
</template>

<script>
import NavigationBar from '@/components/NavigationBar.vue'
import MainPage from '@/components/MainPage.vue'

export default {
  name: 'App',
  components: {
    NavigationBar,
    MainPage
  }
}
</script>

<style>
#app {
  height: 100vh;
}
</style>
