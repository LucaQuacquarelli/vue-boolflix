<template>
    <aside :class="status ? 'active' : ''">
        <input type="text" placeholder="Cerca un Film o una Serie Tv"
        v-if="status"
        @keydown.enter="$emit('search', findedMovie)"
        @keyup.enter="setAside"
        v-model="findedMovie"> 
        <div class="icon-container">
            <div class="btn-container" @click="setAside" :class="status ? 'active' : ''">
                <i class="fas fa-search"></i>
                <span v-if="status">Cerca</span>
            </div>
            <div class="btn-container">
                <i class="fas fa-tv"></i>
                <span v-if="status">Serie Tv</span>
            </div>
            <div class="btn-container">
                <i class="fas fa-film"></i>
                <span v-if="status">Film</span>
            </div>
        </div>
    </aside>
</template>

<script>
export default {
    name: "Aside",
    data: function() {
        return {
            status: false,
            findedMovie: ""
        }
    },
    methods: {
        setAside: function() {
            this.status = !this.status
            this.findedMovie = ""
        }
    }
}
</script>

<style lang="scss" scoped>
@import "~@fortawesome/fontawesome-free/css/all.min.css";
@import "../style/variables";
    aside {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 50px;
        padding: 50px 0;
        background-color:  $menu-bg;
        
        &.active {
            padding: 50px 120px;
        }

        input {
            padding: 10px;
            border-radius: 15px;
            border: 2px solid grey;
            background-color: transparent;
            color: white;
            outline: none;

            &:focus {
                border: 2px solid #db1a28;
            }
        }

        .icon-container {
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            height: 50%;
            margin: 30px 0;

            .btn-container {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                text-align: center;

                &.active {
                    padding: 0 80px;
                }
                
                i {
                    margin: 5px 0;
                    cursor: pointer;
                }
            }

        }    

        
    }
</style>