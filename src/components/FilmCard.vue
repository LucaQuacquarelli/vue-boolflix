<template>
    <div class="card" @mouseup="$emit('setPlay', play)" @click="setTrailer">
        <img :src="item.poster_path" :alt="item.title">
        <div class="card-info">
            <h5>Titolo: <span>{{item.title}}{{item.name}}</span></h5>
            <h6>Titolo originale: <span>{{item.original_title}}{{item.original_name}}</span></h6>
            <h6>Lingua: <span>{{item.original_language}}</span></h6>
            <h6>Voto: <span>{{item.vote_average}}</span></h6>
            <h6>Rate: 
                <span>
                    <i class="fas fa-star"
                    v-for="index in stars" :key="index"
                    ></i>
                </span>
                <span>
                    <i  v-for="index in (5 - stars)" 
                        :key="index" 
                        class="far fa-star"></i>
                </span>
            </h6>
        </div>
    </div>
    
</template>

<script>
export default {
    name: "FilmCard",
    props: {
        item: Object,
        stars: Number
    },
    data: function() {
        return {
            play: true
        }
    },
    methods: {
        setTrailer: function() {
            this.play = !this.play
        }
    }
}
</script>

<style lang="scss" scoped>
@import "../style/variables";

    .card {
        width: 130px;
        height: 200px;
        margin: 10px;
        position: relative;
        cursor: pointer;

        img {
            width: 100%;
            height: 100%;
        }

        &:hover .card-info {
            display: block;
        }

        .card-info {
            display: none;
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            padding: 15px;
            color: $color-theme;
            background-color: rgba($menu-bg, 0.8);

            & h6 {
                margin: 5px 0;
            }

            & span {
                color: white;
            }

        }

    }
    
</style>