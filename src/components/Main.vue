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
                :item="movie"/>
            </div>
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
    }
    
}
</script>

<style lang="scss" scoped>
    main {
        width: 100%;
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
        }

        .film-container {
            display: flex;
            flex-wrap: wrap;
            margin: 20px 0;
        }
    }
</style>