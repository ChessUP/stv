<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <ClientList></ClientList>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import ClientList from './components/ClientList.vue'
// import QRCode from 'qrcode-generator'




export default {
  watch: {
  },
  name: 'App',
  components: {
    // HelloWorld,
    ClientList
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
