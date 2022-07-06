<template>
  <MainPage/>
</template>

<script>
import MainPage from './components/MainPage.vue'

export default {
  name: 'App',
  components: {
    MainPage
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
}
a {
	text-decoration: none;
	color: black;
	cursor: pointer;
	transition: .1s;
}
a:hover {
	color: #0077ff;
}
</style>
