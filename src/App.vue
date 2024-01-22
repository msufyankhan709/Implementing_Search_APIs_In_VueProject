<template>
  <div>
    <SearchApp />
    <UserApp/>
  </div>
</template>

<script>
import SearchApp from './components/Search.vue'
import UserApp from './components/User.vue'

export default {
  name: 'App',
  components: {
    SearchApp,
    UserApp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
