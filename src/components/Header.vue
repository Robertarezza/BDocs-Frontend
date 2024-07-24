<script>
import { RouterLink } from "vue-router";
import { store } from "../store.js";

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
            <ul>
                <li class="box-img">
                    <router-link :to="{ name: 'home' }">
                        <img src="../assets/img/logo-1.png" alt="logo B-Doctors">
                    </router-link>
                </li>
                <li id="title">
                    <a href="#footer">Contattaci</a>
                </li>
            </ul>
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

    .test{
        list-style-type: none;
    }

    nav {
        width: 100%;
        padding: 20px;
        height: 100%;

        ul {
            display: flex;
            justify-content: space-between;
            align-items: center;


            .box-img {
                display: flex;
                justify-content: start;

                img {
                    //height: 60px;
                    //display: block;
                    max-width: 45%;
                    //aspect-ratio: 1;
                }
            }

            #title {
                list-style-type: none;

                a {
                    text-decoration: none;
                    color: white;
                }
            }
        }
    }
}
</style>
