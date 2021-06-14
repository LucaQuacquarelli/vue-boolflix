<template>
    <main>
        <h2>Risultati per '{{search}}'</h2>
        <div class="film-container">
            <FilmCard/>
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
            finded: "."
        }
    },
    methods: {
        setFinded: function() {
            this.finded = this.search
        }
    },
    updated: function() {
        axios
            .get("https://api.themoviedb.org/3/search/movie", {
                params: {
                    api_key: "ffe0662e93ba06b23193db8072b78d11",
                    query: this.finded
                }
            })
            .then(
                (res) => {
                    console.log(res.data);
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
            height: 300px;
            margin: 20px 0;
        }
    }
</style>