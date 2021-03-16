<template>
  <div id="app">
    <app-header ></app-header>
    <app-mainview v-bind:categories="categories"></app-mainview>
    <app-footer></app-footer>
    <!-- <router-view></router-view> -->
  </div>
</template>

<script>
import Header from './assets/components/Header'
import Footer from './assets/components/Footer'
import MainView from './assets/components/MainView'
import categories from './assets/components/categories'

export default {
  
  components:{
    "app-header": Header,
    "app-mainview": MainView,
    "app-footer": Footer
  },

  data () {
    return {
      categories,
    }
  }
}
</script>

<style>

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Open sans';
  font-size: 20px;
}

</style>
