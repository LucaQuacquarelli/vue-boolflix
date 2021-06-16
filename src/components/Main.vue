<template>
    <main>
        <div class="home" v-if="movies.length == 0 && series.length == 0">
            <div class="home-text" v-if="!searching">
                <h1>Film, serie TV e tanto altro. <br> Senza limiti.</h1>
                <p>Guarda ciò che vuoi ovunque.</p>
            </div>
            <h1 v-if="searching">La ricerca non ha prodotto risultati per '{{search}}'</h1>
        </div>
        <div class="searched-container"  v-show="movies.length > 0 && series.length > 0">
            <h3>Risultati per '{{search}}'</h3>
            <section class="films-container">
                <h2>Film</h2>
                <div class="films">
                    <FilmCard v-for="movie in movies" :key="movie.id"
                    :item="movie"
                    :stars="getStars(movie.vote_average)"
                    @setPlay="showTrailer"/>
                </div>
            </section>
            <section class="series-container">
                <h2>Serie Tv</h2>
                <div class="series">
                    <FilmCard v-for="serie in series" :key="serie.id"
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
        search: String,
        stop: Boolean,
        searching: Boolean 
    },
    data: function() {
        return {
            trailer: false
        }
    },
    methods: {
        getStars(number) {
            return Math.floor(parseInt(number) / 2);
        },
        showTrailer: function(play) {
            this.trailer = play
            this.stop = play
        }
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

        .searched-container {
            padding: 50px 20px;
            
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