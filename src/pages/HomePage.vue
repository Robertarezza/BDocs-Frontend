<script>
import axios from "axios"; 
import { store } from '../store.js'; 
import DoctorCard from "../components/DoctorCard.vue";
import SearchBar from '../components/SearchBar.vue';

export default {
    components: {
        DoctorCard, 
        SearchBar,
    },

    data() {
        return {
            doctors: null,
            store,
        };
    },

    created() {
        axios.get(`${this.store.apiBaseURL}/api/doctors`)
            .then((resp) => {
                this.doctors = resp.data.results; 
                this.$nextTick(() => {
                    this.handleScroll();
                });
            })
            .catch(error => {
                console.error('Errore fetch dottori:', error); 
            });
    },

    mounted() {
        window.addEventListener('scroll', this.handleScroll);
    },

    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },

    methods: {
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
        <section class="welcome-section">
            <div class="welcome-text">
                <h1 class="typewriter">Benvenuti nel nostro Studio Medico</h1>
                <p class="typewriter">Offriamo i migliori professionisti medici per la vostra salute.</p>
            </div>
        </section>
        <div class="d-flex justify-content-center">
            <SearchBar />
        </div>
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
    from { width: 0 }
    to { width: 100% }
}

@keyframes blink-caret {
    from, to { border-color: transparent }
    50% { border-color: rgba(146, 180, 244, 1); }
}

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
</style>

