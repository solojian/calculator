<template>
  <div id="app">
    <div id="swiper">
        <v-header></v-header>
        <v-container></v-container>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Container from './components/Container.vue'

export default {
  name: 'App',
  components: {
    "v-header": Header,
    "v-container": Container
  }
}
</script>

<style>
* {
    margin:0;
    padding:0;
    box-sizing:border-box;
    font:700 18px Arial, sans-serif
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#swiper {
    width:325px;
    height:auto;
    margin:100px auto;
    padding:20px 20px 9px;
    box-sizing: border-box;
    background:#9dd2ea;
    background:linear-gradient(#9dd2ea, #8bceec);
    border-radius:3px;
    box-shadow:0 4px #009de4, 0 10px 15px rgba(0, 0, 0, .2)
}
</style>
