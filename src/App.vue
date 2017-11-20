<template>
  <div class="container" id="app">
    <NewsList></NewsList>

  </div>
</template>

<script>
import NewsList from './components/NewsList'
export default {
  name: 'app',
  components: {
    NewsList
  }
}
</script>

<style>
#app {
  padding-top: 20px;
}
</style>
