<template>
  <div id="app">
    <Header/>
    <div class="app-container">
      <Aside @search="searchMovie"/>
      <Main
      :search="finded"/>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Aside from './components/Aside.vue'
import Main from './components/Main.vue'


export default {
  name: 'App',
  components: {
    Aside,
    Header,
    Main
    
  },
  data: function() {
    return {
      finded: ""
    }
  },
  methods: {
    searchMovie: function(findedMovie) {
      this.finded = findedMovie
    }
  }
}
</script>

<style lang="scss">
  @import "./style/general";
    
    #app {
      height: 100%;

      .app-container {
        display: flex;
        height: calc(100% - 80px);
      }

    }

  
  
</style>
