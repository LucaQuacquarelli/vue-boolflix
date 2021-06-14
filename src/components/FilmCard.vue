<template>
    <div class="card">
        <div class="card-info">
            <h4>Titolo:</h4>
            <h5>Titolo originale:</h5>
            <h6>Lingua:</h6>
            <h6>Voto:</h6>
        </div>
    </div>
</template>

<script>
export default {
    name: "FilmCard",
}
</script>

<style lang="scss" scoped>
@import "../style/variables";

    .card {
        width: 130px;
        height: 200px;
        padding: 15px;

        &:hover .card-info {
            display: block;
        }

        .card-info {
            display: none;
            background-color: rgba($menu-bg, 0.4);
            
            & * {
                margin: 5px 0;
            }
        }

    }
</style>