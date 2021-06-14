<template>
    <main>
        <h2>Risultati per '{{search}}'</h2>
        <div class="film-container">
            <FilmCard v-for="(movie, index) in movies" :key="index"
            :cover="movie.poster_path"
            :title="movie.title"
            :originalTitle="movie.original_title"
            :language="movie.original_language"
            :vote="movie.vote_average"/>
        </div>
    </main>
</template>

<script>
import axios from "axios"
import FilmCard from './FilmCard.vue';

export default {
    name: "Main",
    components: {
        FilmCard,
    },
    props: {
        search: String,
    },
    data: function() {
        return {
            movies: []
        }
    },
    updated: function() {
        axios
            .get("https://api.themoviedb.org/3/search/movie", {
                params: {
                    api_key: "ffe0662e93ba06b23193db8072b78d11",
                    query: this.search
                }
            })
            .then(
                (res) => {

                    var result = res.data.results;

                    result.forEach(
                        (element) => {
                        if (element.original_language == "it") {
                            element.original_language = "🇮🇹"
                        } else if (element.original_language == "en") {
                            element.original_language = "🇬🇧"
                        }
                    });
                    

                    this.movies = result;
                    
                }
            )
            
    }
}
</script>

<style lang="scss" scoped>
    main {
        width: 100%;
        padding: 50px 20px;
        overflow-y: auto;

        .film-container {
            display: flex;
            flex-wrap: wrap;
            height: 300px;
            margin: 20px 0;
        }
    }
</style>