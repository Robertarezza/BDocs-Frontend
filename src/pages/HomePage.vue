<script>
import axios from 'axios'

export default {
    data() {
        return {

        }
    },

    created() {
        axios.get('http://127.0.0.1:8000/api/doctors').then((response) => {
            console.log(response);
        })
    }
}
</script>

<template>
    <div class="">
        Ciao a tutti
    </div>
</template>

<style scoped lang="scss">
@use "../style/partials/variables" as *;

div {
    height: 100vh;
    background: $gradient-top;
}
</style>