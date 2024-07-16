<script>
export default {
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

    nav {
        z-index: 9999;
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