<template>
    <header>
        <img src="../assets/netflix-logo.png" alt="Netflix Logo">
        <div class="user-container">
            <i class="fas fa-bell"></i>
            <div class="user">LQ</div>
            <span>Luca Quacquarelli</span>
        </div>
    </header>
</template>

<script>
export default {
    name: "Header",

}
</script>

<style lang="scss" scoped>
@import "../style/variables";
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 80px;
        padding: 10px;
        background-color: $menu-bg;

        img {
            height: 100%;
        }
        
        .user-container {
            display: flex;
            align-items: center;
            
            .user {
                display: flex;
                justify-content: center;
                align-items: center;
                width: 25px;
                height: 25px;
                margin: 0 15px;
                background-color: $color-theme;
                border-radius: 50%;
                font-size: 12px;
            }

        }

        

    }
</style>