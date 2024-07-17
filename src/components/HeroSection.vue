<script>
import axios from "axios";
import { store } from '../store.js';
export default {
    data() {
        return {
            specializations: [],
            doctors: null,
            store,
            selectSpecialization: ""
        }
    },
    created() {
        this.getDoctors();
        this.getSpecialization();
    },
    methods: {
        getSpecialization() {
            axios.get(`${this.store.apiBaseURL}/api/specializations`).then((resp) => {
                console.log(resp);
                this.specializations = resp.data.results;
            })
        },
        getDoctors() {
            const params = {};
            if (this.selectSpecialization !== "") {
                params.specialization_id = this.selectSpecialization
            }
            axios.get(`${this.store.apiBaseURL}/api/doctors`, {
                params
            })
                .then((resp) => {
                    this.doctors = resp.data.results;
                    console.log(this.doctors);
                    this.$nextTick(() => {
                        this.handleScroll();
                    });
                })
                .catch(error => {
                    console.error('Errore fetch dottori:', error);
                });
        }
    }
}
</script>


<template>

    <div class="hero">
        <section class="welcome-section">
            <div class="welcome-text">
                <h1 class="typewriter">Benvenuti nel nostro Studio Medico</h1>
                <p class="typewriter">Offriamo i migliori professionisti medici per la vostra salute.</p>
            </div>
        </section>

        <div class="custom-select">
            <select id="" aria-label="seleziona specializzazione" v-model="selectSpecialization" @change="getDoctors">
                <option value="">Tutte le specializzazioni</option>
                <option :value="specialization.id" v-for="specialization in specializations"> {{ specialization.title }}
                </option>
            </select>
        </div>
    </div>

</template>


<style lang="scss" scoped>
@use "../style/partials/variables" as *;

.hero {
    margin-top: 100px;
    height: 600px;
    background-image: url(../assets/img/nursing3.jpg);
    background-size: cover;
    margin-bottom: 20px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: end;

    .custom-select {
        margin-top: 20px;
        width: 70%;
        display: flex;
        justify-content: center;

        select {
            border-radius: 10px;
            padding: 10px;
            border: 2px solid $glaucous;
            color: $glaucous;
            background-color: transparent;
        }
    }
}

/* Sezione di benvenuto */
.welcome-section {
    background: url('path/to/your/background.jpg') no-repeat center center;
    background-size: cover;
    padding-top: 150px;
    color: rgba(10, 54, 157, 1);
    text-align: center;
    animation: slide-down 1s ease-out;

    .welcome-text {
        display: inline-block;
        padding: 20px;
        border-radius: 10px;
    }
}

/* Animazione per la sezione di benvenuto */
@keyframes slide-down {
    from {
        transform: translateY(-50px);
        opacity: 0;
    }

    to {
        transform: translateY(0);
        opacity: 1;
    }
}

/* Effetto di scrittura per il testo della sezione di benvenuto */
.typewriter {
    overflow: hidden;
    border-right: 5px solid rgba(146, 180, 244, 1);
    white-space: nowrap;
    margin: 0 auto;
    letter-spacing: .15em;
    animation: typing 3.5s steps(40, end), blink-caret .75s;
}

@keyframes typing {
    from {
        width: 0
    }

    to {
        width: 100%
    }
}

@keyframes blink-caret {

    from,
    to {
        border-color: transparent
    }

    50% {
        border-color: rgba(146, 180, 244, 1);
    }
}
</style>