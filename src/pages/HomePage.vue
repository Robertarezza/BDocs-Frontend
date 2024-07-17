<script>
import axios from "axios"; 
import { store } from '../store.js'; 
import DoctorCard from "../components/DoctorCard.vue"; 

export default {
    components: {
        DoctorCard, 
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
                console.log(this.doctors);
            })
            .catch(error => {
                console.error('Error fetching doctors:', error); 
            });
    },
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
        <div class="container mt-5 mb-5">
            <h1 class="text-center mb-3 typewriter-doc">I nostri Dottori</h1>
            <p class="text-center mb-5 typewriter-doc">Il nostro team di medici altamente qualificati è qui per prendersi cura di voi.</p>
           <!-- cord doctor -->
            <div v-if="doctors" class="doctors-grid">
                <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-3">
                    <div class="col-12" v-for="doctor in doctors" :key="doctor.id" v-bind:class="{ 'fade-in': true }">
                        <DoctorCard :doctor="doctor" />
                    </div>
                </div>
            </div>
            <!-- /cord doctor -->
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
    // padding: 150px 0;
    padding-top: 150px;
   // padding-bottom: 50px;
    color:  rgba(10, 54, 157, 1);
    text-align: center;
    animation: slide-down 1s ease-out;

    .welcome-text {
        //background: rgba(0, 0, 0, 0.5);
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
    border-right: 5px solid rgba(146, 180, 244, 1); /* Carattere di cursore */
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
    //border-right: 5px solid rgba(146, 180, 244, 1); /* Carattere di cursore */
    white-space: nowrap;
    margin: 0 auto; 
    letter-spacing: .15em; 
    animation: typing 3.5s steps(40, end), blink-caret .75s;
    color:  rgba(10, 54, 157, 1);
}

@keyframes typing {
    from { width: 0 }
    to { width: 100% }
}

@keyframes blink-caret {
    from, to { border-color: transparent }
    50% { border-color: rgba(146, 180, 244, 1); }
}

// .container {
//     min-height: 100vh;
//     background: $gradient-top;
//     padding-top: 50px;
//     padding-bottom: 50px;
// }


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

/* Stile e animazione per le schede dei dottori */
.doctors-grid .col-12 {
    opacity: 0; 
    transform: translateY(30px); 
    animation: fade-in 0.15s ease-out forwards; 
    animation-delay: calc(0.10s * var(--i)); 
}

/* Animazione di dissolvenza per le schede dei dottori */
@keyframes fade-in {
    to {
        opacity: 1; 
        transform: translateY(0); 
    }
}

/* Scorrimento fluido */
html {
    scroll-behavior: smooth; /* Abilita lo scorrimento fluido */
}
</style>
