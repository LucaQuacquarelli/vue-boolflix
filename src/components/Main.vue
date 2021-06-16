<template>
    <main>
        <div class="home" v-if="movies.length == 0 && series.length == 0">
            <div class="home-text" v-if="!searching">
                <h1>Film, serie TV e tanto altro. <br> Senza limiti.</h1>
                <p>Guarda ciò che vuoi ovunque.</p>
            </div>
            <h1 v-if="searching">La ricerca non ha prodotto risultati per '{{search}}'</h1>
        </div>
        <div class="genres-nav" v-if="searching">
            <ul>
                <li @click="resetActive" :class="activeIndex != -1 ? '': 'active'">All</li>
                <li v-for="(genre, index) in genres"
                :key="genre.id"
                :class="index == activeIndex ? 'active': ''" @click="setActive(index)">{{genre.name}}</li>
            </ul>
        </div>
        <div class="searched-container"  v-show="movies.length > 0 || series.length > 0">
            <h3>Risultati per '{{search}}'</h3>
            <section class="films-container">
                <h2 v-if="filterMovieGenres.length > 0">Film</h2>
                <h2 v-else>Non ci sono film in questa categoria</h2>
                <div class="films">
                    <FilmCard v-for="movie in filterMovieGenres" :key="movie.id"
                    :item="movie"
                    :stars="getStars(movie.vote_average)"
                    @setPlay="showTrailer"/>
                </div>
            </section>
            <section class="series-container">
                <h2 v-if="filterSeriesGenres.length > 0">Serie Tv</h2>
                <h2 v-else>Non ci sono serie tv in questa categoria</h2>
                <div class="series">
                    <FilmCard v-for="serie in filterSeriesGenres" :key="serie.id"
                    :item="serie"
                    :stars="getStars(serie.vote_average)"
                    @setPlay="showTrailer"/>
                </div>
            </section>
        </div>
        <div class="trailer-container" v-if="trailer && stop">
            <video controls autoplay>
                <source src="../assets/video/trailer.mp4" type="video/mp4">
            </video>
        </div>
    </main>
</template>

<script>
import FilmCard from './FilmCard.vue';

export default {
    name: "Main",
    components: {
        FilmCard,
    },
    props: {
        movies: Array,
        series: Array,
        genres: Array,
        search: String,
        stop: Boolean,
        searching: Boolean 
    },
    data: function() {
        return {
            trailer: false,
            activeIndex: -1,
            currentGenre: 0
        }
    },
    computed: {
        filterMovieGenres: function() {

            if (this.currentGenre == 0) {
                return this.movies
            }

            const newArray = this.movies.filter(
                (element) => {
                    return element.genre_ids.includes(this.currentGenre);  
                }
            )
            return newArray;
        },
        filterSeriesGenres: function() {

            if (this.currentGenre == 0) {
                return this.series
            }

            const newArray = this.series.filter(
                (element) => {
                    return element.genre_ids.includes(this.currentGenre);  
                }
            )
            return newArray;
        }
    },
    methods: {
        getStars(number) {
            return Math.floor(parseInt(number) / 2);
        },
        showTrailer: function(play) {
            this.trailer = play
            this.stop = play
        },
        setActive: function(newIndex) {
            this.activeIndex = newIndex

            switch (this.activeIndex) {

                case 0:
                    this.currentGenre = 28
                break;
                case 1:
                    this.currentGenre = 12
                break;
                case 2:
                    this.currentGenre = 16
                break;
                case 3:
                    this.currentGenre = 35
                break;
                case 4:
                    this.currentGenre = 80
                break;
                case 5:
                    this.currentGenre = 99
                break;
                case 6:
                    this.currentGenre = 18
                break;
                case 7:
                    this.currentGenre = 10751
                break;
                case 8:
                    this.currentGenre = 14
                break;
                case 9:
                    this.currentGenre = 36
                break;
                case 10:
                    this.currentGenre = 27
                break;
                case 11:
                    this.currentGenre = 10402
                break;
                case 12:
                    this.currentGenre = 9648
                break;
                case 13:
                    this.currentGenre = 10749
                break;
                case 14:
                    this.currentGenre = 878
                break;
                case 15:
                    this.currentGenre = 10770
                break;
                case 16:
                    this.currentGenre = 53
                break;
                case 17:
                    this.currentGenre = 10752
                break;
                case 18:
                    this.currentGenre = 37
                break;
                case 19:
                    this.currentGenre = 10762
                break;
                case 20:
                    this.currentGenre = 10763
                break;
                case 21:
                    this.currentGenre = 10764
                break;
                case 22:
                    this.currentGenre = 10765
                break;
                case 23:
                    this.currentGenre = 10766
                break;
                case 24:
                    this.currentGenre = 10767
                break;
                case 25:
                    this.currentGenre = 10768
                break;
                case 26:
                    this.currentGenre = 10770
                break;
            }
        },
        resetActive: function() {
            this.activeIndex = -1
            this.currentGenre = 0
        },
    }
    
}
</script>

<style lang="scss" scoped>
@import "../style/variables";
    main {
        width: 100%;
        position: relative;
        overflow-y: auto;

        .home {
            display: flex;
            flex-direction: column;
            justify-content: center;
            height: 100%;
            background-image: url("https://assets.nflxext.com/ffe/siteui/vlv3/c0a32732-b033-43b3-be2a-8fee037a6146/ac84d843-0e4d-4bff-9992-7dd636827a40/IT-it-20210607-popsignuptwoweeks-perspective_alpha_website_small.jpg");
            background-size: cover;
            text-align: center;

            & h1 {
                margin: 25px 0;
                font-size: 50px;
            }

            & p {
                font-size: 30px;
            }
        }

        .genres-nav {
            padding: 10px;

            ul {
                list-style: none;

                li {
                    display: inline-block;
                    margin: 0 10px;
                    padding: 10px 0;
                    cursor: pointer;

                    &:hover,
                    &.active {
                        color:  $color-theme;
                    }
                }
            }

        }

        .searched-container {
            padding: 25px 20px;
            
            h2 {
                margin: 20px 0;

            }

            .films,
            .series {
                display: flex;
                flex-wrap: wrap;
            }
        }

        .trailer-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 500px;
            height: 250px;
            z-index: 2;

            video {
                width: 100%;
                height: 100%;
            }
        }
    }
</style>