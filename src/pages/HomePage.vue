<script>
import axios from "axios"; 
import { store } from '../store.js'; 
import DoctorCard from "../components/DoctorCard.vue";
import SearchBar from '../components/SearchBar.vue';
import HeroSection from "../components/HeroSection.vue";

export default {
    components: {
        DoctorCard, 
        SearchBar,
        HeroSection
    },

    data() {
        return {
            specializations: [],
            doctors: null,
            store,
            selectSpecialization: "",
        };
    },

    created() {
        this.getDoctors();
        this.getSpecialization();
    },

    mounted() {
        window.addEventListener('scroll', this.handleScroll);
    },

    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },

    methods: {
        getDoctors() {
            const params = {};
            if (this.selectSpecialization !== "") {
                params.specialization_id = this.selectSpecialization
            }
            axios.get(`${this.store.apiBaseURL}/api/doctors`,  {
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
        },
        getSpecialization() {
            axios.get(`${this.store.apiBaseURL}/api/specializations`).then((resp) => {
                console.log(resp);
                this.specializations = resp.data.results;
            }) 
        },
        handleScroll() {
            const cards = document.querySelectorAll('.fade-in');
            const windowHeight = window.innerHeight;

            cards.forEach(card => {
                const rect = card.getBoundingClientRect();
                if (rect.top < windowHeight && rect.bottom > 200) { 
                    card.classList.add('visible');
                } else {
                    card.classList.remove('visible');
                }
            });
        }
    }
};
</script>


<template>
    <div>

        <!-- HERO SECTION -->
        <HeroSection />

        <!-- SEARCH BAR -->
        <div class="d-flex justify-content-center custom-select">
            <!-- <SearchBar /> -->
            <select id="" aria-label="seleziona specializzazione"
            v-model="selectSpecialization"
            @change="getDoctors">
                <option value="">Tutte le specializzazioni</option>
                <option :value="specialization.id" v-for="specialization in specializations"> {{ specialization.title }} </option>
            </select>
        </div>
        <!-- /SEARCH BAR -->

        <div class="container mt-5 mb-5">
            <h1 class="text-center mb-3 typewriter-doc">I nostri Dottori</h1>
            <p class="text-center mb-5 typewriter-doc">Il nostro team di medici altamente qualificati è qui per prendersi cura di voi.</p>
            <div v-if="doctors" class="doctors-grid">
                <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-3">
                    <div class="col-12 fade-in" v-for="doctor in doctors" :key="doctor.id">
                        <DoctorCard :doctor="doctor" />
                    </div>
                </div>
            </div>
            <div v-else>
                <div class="loader">
                    <span class="loader-text">caricamento</span>
                    <span class="load"></span>
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped lang="scss">
@use "../style/partials/variables" as *;

/* Effetto di scrittura per il testo della i nostri dottori */
.typewriter-doc {
    overflow: hidden;
    white-space: nowrap;
    margin: 0 auto; 
    letter-spacing: .15em; 
    animation: typing 3.5s steps(40, end), blink-caret .75s;
    color: rgba(10, 54, 157, 1);
}

@keyframes typing {
    from { width: 0 }
    to { width: 100% }
}

@keyframes blink-caret {
    from, to { border-color: transparent }
    50% { border-color: rgba(146, 180, 244, 1); }
}

.card-img-top {
    object-fit: cover;
    height: 200px;
    border-radius: 10px;
}

.card-body {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
    overflow: hidden;
}

.card-text ul {
    padding-left: 20px;
    list-style: disc;
}

.loader {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

.loader-text {
    margin-right: 10px;
}

.load {
    border: 2px solid $egyptian-blue;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

html {
    scroll-behavior: smooth; 
}

// Tentativo di fade-in delle cards
.fade-in {
    opacity: 0; 
    transition: opacity 1s cubic-bezier(0.25, 0.1, 0.25, 1); 
}

.fade-in.visible {
    opacity: 1; 
}

// Tentativo di fae in delle cards

//Select custom
select {
    border-radius: 10px;
    padding: 10px;
    border: 2px solid $glaucous;
    color: $glaucous;
}

</style>

