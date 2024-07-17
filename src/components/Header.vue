<script>
import SearchBar from './SearchBar.vue';

export default {
    components: {
        SearchBar,
    },
    data() {
        return {

        }
    },
}
</script>

<template>
    <header>
        <nav>
            <div class="box-img">
                <img src="../assets/img/logo.png" alt="logo B-Doctors">
            </div>
            <SearchBar />
            <div id="title">
                <h3>B-Doctors</h3>
            </div>
        </nav>
    </header>
</template>




<style scoped lang="scss">
@use "../style/partials/variables" as *;

header {
    height: 100px;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: $celtic-blue;
    z-index: 9999;

    nav {
       
        width: 100%;
        padding: 20px;
        height: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .box-img {
            display: flex;
            justify-content: start;

            img {
                height: 60px;
                display: block;
                max-width: 100%;
                aspect-ratio: 1;

            }
        }
        #title {
            color: white;
        }
    }
}
</style>