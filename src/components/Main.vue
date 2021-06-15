<template>
    <main>
        <div class="home" v-if="movies.length == 0">
            <h1>Film, serie TV e tanto altro. <br> Senza limiti.</h1>
            <p>Guarda ciò che vuoi ovunque.</p>
        </div>
        <div class="searched-container"  v-show="movies.length > 0">
            <h2>Risultati per '{{search}}'</h2>
            <div class="film-container">
                <FilmCard v-for="movie in movies" :key="movie.id"
                :item="movie"
                :stars="getStars(movie.vote_average)"
                @setPlay="showTrailer"/>
            </div>
        </div>
        <div class="trailer-container" v-if="trailer">
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
        search: String
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
            
            .film-container {
                display: flex;
                flex-wrap: wrap;
                margin: 20px 0;
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