<template>
  <div id="app">
    <Header/>
    <div class="app-container">
      <Aside @search="searchMovie" @home="returnHome" @stop="setTrailer"/>
      <Main
      :movies="films"
      :search="finded"
      :series="series"
      :stop="stopTrailer"
      :searching="searchStarted"
      :genres="genresArray"/>
    </div>
  </div>
</template>

<script>
import axios from "axios"
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
      films: [],
      series: [],
      genresArray: [],
      finded: "",
      stopTrailer: false,
      searchStarted: false
    }
  },
  methods: {
    searchMovie: function(findedMovie) {
      axios.all([
        axios
          .get("https://api.themoviedb.org/3/search/movie",{
            params: {
              api_key: "ffe0662e93ba06b23193db8072b78d11",
              query: findedMovie
            }
          }),
        
        axios
          .get("https://api.themoviedb.org/3/search/tv",{
            params: {
              api_key: "ffe0662e93ba06b23193db8072b78d11",
              query: findedMovie
            }
          })
      ])
          .then (axios.spread((...res) => {
            var answers = res[0].data.results.concat(res[1].data.results);

            answers.forEach(
              (element) => {

                if (element.original_language == "it") {
                  element.original_language = "🇮🇹"
                } else if (element.original_language == "en") {
                  element.original_language = "🇬🇧"
                }

                if (element.poster_path == null) {
                  element.poster_path = "https://i.pinimg.com/originals/a0/25/5d/a0255d73a758bf7b8eaf81e07e8f125d.jpg"
                } else {
                  element.poster_path = `https://image.tmdb.org/t/p/w342/${element.poster_path}`
                }

              });

            this.films = res[0].data.results
            this.series = res[1].data.results
            this.finded = findedMovie
            this.searchStarted = true
          }))
    },
    returnHome: function() {
      this.films = []
      this.series = []
      this.finded = ""
      this.searchStarted = false
    },
    setTrailer: function(trailer) {
      this.stopTrailer = trailer
    }
  },
  created: function() {

    axios.all([
      axios
        .get("https://api.themoviedb.org/3/genre/movie/list",{
          params: {
            api_key: "ffe0662e93ba06b23193db8072b78d11"
          }
      }),
      
      axios
        .get("https://api.themoviedb.org/3/genre/tv/list",{
          params: {
            api_key: "ffe0662e93ba06b23193db8072b78d11"
          }
      })
    ])
      
      .then(axios.spread((...res) => {
          var answers = res[0].data.genres.concat(res[1].data.genres)
          
          const newArray = []
          const newObject = {}

          
          answers.forEach(
            (element) => {
              let objId = element['id']
              newObject[objId] = element
            }
          )

          for (let i in newObject) {
            newArray.push(newObject[i]);
          }
          this.genresArray = newArray
        }))
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
