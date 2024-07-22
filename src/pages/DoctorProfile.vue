<script>
import axios from "axios";
import { store } from "../store.js";
import CardProfile from "../components/CardProfile.vue";
import PreFooter from "../components/PreFooter.vue";
import Review from "../components/Review.vue";
import Message from "../components/Message.vue";
import Votes from "../components/Votes.vue";

export default {
  components: {
    CardProfile,
    PreFooter,
    Review,
    Message,
    Votes,
  },

  data() {
    return {
      doctor: null,
      store,
    };
  },
  computed: {
    averageRating() {
      // Calcola la media dei voti se i voti sono disponibili
      if (this.doctor.ratings && this.doctor.ratings.length > 0) {
        const total = this.doctor.ratings.reduce((sum, rating) => sum + rating.rating, 0);
        return total / this.doctor.ratings.length;
      }
      return 0;
    },
  },
  created() {
    const id = this.$route.params.id;
    axios
      .get(`${store.apiBaseURL}/api/doctors/${id}`)
      .then((resp) => {
        console.log(resp);
        this.doctor = resp.data.results;
        console.log(this.doctor);
      })
      .catch((error) => {
        console.error("Error fetching doctors:", error);
      });
  }
};
</script>

<template>
  <!-- loader -->
  <div class="loader-container d-none">
    <div class="loader"></div>
  </div>

  <div class="container-fluid cont-top">
    <div class="row align-items-center ms_style">
      <div class="card mb-3" style="max-width: 1000px">
        <div class="row g-0">
          <div class="col-md-4">
            <img :src="doctor.photo
              ? `${store.imageUrl}/${doctor.photo}`
              : `https://t3.ftcdn.net/jpg/02/48/42/64/360_F_248426448_NVKLywWqArG2ADUxDq6QprtIzsF82dMF.jpg`
              " class="card-img-top" alt="Doctor Photo" style="max-width: 100%" />
          </div>
          <div class="col-md-8 align-content-center">
            <!-- Stelline sopra la foto -->
            <div class="rating-stars">
              <span v-for="star in 5" :key="star" class="star" :class="{ filled: star <= averageRating }">
                ★
              </span>
            </div>
            <!-- /stelline sopra la foto -->
            <div class="card-body">
              <h1>{{ doctor.user.name }} {{ doctor.user.surname }}</h1>
              <span>Specializzazione </span>
              <div class="d-inline">
                <span class="text-secondary" v-for="(specialization, index) in doctor.specializations"
                  :key="specialization.id">
                  <template v-if="index > 0"> e </template>
                  <strong>{{ specialization.title }}</strong>
                </span>
                <br />
                <span> Tipo di prestazione: </span>
                <span class="text-secondary"><strong>{{ doctor.performance }}</strong></span>
              </div>
              <div class="mt-2">
                <p class="m-0">
                  <i class="fa-solid fa-location-dot"></i> {{ doctor.studio_address }}
                </p>
                <p class="m-0">
                  <i class="fa-solid fa-address-card"></i> {{ doctor.user.email }}
                </p>
                <p class="m-0">
                  <i class="fa-solid fa-phone"></i> {{ doctor.phone_number }}
                </p>
                <a :href="`${store.apiBaseURL}/storage/${doctor.CV}`" target="_blank" class="text-primary">
                  Guarda il CV
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <transition name="fade">
    <div class="alert alert-success ms-alert-success" v-if="store.successMessage">
      Il tuo messaggio è stato inviato con successo
    </div>
  </transition>
  <div class="container cont-card">
    <CardProfile :doctor="doctor" />
  </div>

  <div class="d-none">
    <Review :doctor="doctor.user.id" />
  </div>
  <div class="d-none">
    <Message :doctor="doctor.user.id" />
  </div>
  <div class="d-none">
    <Votes :doctor="doctor.user.id" />
  </div>

  <div class="d-inline">
    <div class="text-secondary" v-for="(review, index) in doctor.reviews" :key="review.id">
      <template v-if="index > 0"> e </template>
      <strong>Nome {{ review.guest_name }}</strong>
      <strong>Nome {{ review.guest_mail }}</strong>
      <strong>Nome {{ review.review }}</strong>
    </div>
  </div>

  <PreFooter />
</template>

<style scoped lang="scss">
.cont-top {
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0), rgba(255, 255, 255, 1)),
    url(../assets/img/nursing4.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
}

.loader-container {
  z-index: 9999;
  padding: 30px;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

//loader
.loader {
  border: 12px solid #f3f3f3;
  border-radius: 50%;
  border-top: 12px solid #3498db;
  width: 70px;
  height: 70px;

  -webkit-animation: spin 2s linear infinite;
  /* Safari */
  animation: spin 2s linear infinite;
}

/* Safari */
@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
  }

  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/* Stelline sopra la foto */
.rating-stars {
  // position: absolute;
  //top: -3px;
  //left: 106px;
  display: flex;
  //z-index: 1;
  margin-left: 15px;
}

.star {
  font-size: 20px;
  color: grey;
  margin-right: 2px;
}

.star.filled {
  color: gold;
}

img {
  mix-blend-mode: multiply;
}

.ms_style {
  justify-content: center;
  margin-top: 100px;
  padding-top: 10px;

  .card {
    border: none;
    background-color: transparent;
    padding-top: 50px;
  }
}

.user-picture {
  max-width: 200px;
  margin: 0 auto;
}

span {
  font-weight: 900;
  font-style: italic;
}

.cont-card {
  margin: 0 auto;
  margin-bottom: 50px;
}

// Bottone messaggio, animazioni custom in entrata e ucita
.ms-alert-success {
  position: fixed;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  // SE CI SONO PROBLEMI CON IL BACGROUNG DI ALLERT .alert-success, è questa opzione il problema
  background-color: rgba(212, 237, 218, 0.9);
  padding: 15px 30px;
  border-radius: 5px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  transition: opacity 0.5s ease-in-out;
  opacity: 1;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

/* Breakpoint 1024px */
@media (max-width: 1024px) {
  .cont-top {
    background-attachment: scroll;
  }

  .ms_style .card {
    padding-top: 30px;
  }

  .profile-header {
    flex-direction: column;
    align-items: center;
  }

  .card-body {
    text-align: center;
  }

  .card-img-top {
    width: 80%;
    margin: 0 auto;
  }
}

/* Breakpoint 768px */
@media (max-width: 768px) {
  .ms_style .card {
    padding-top: 20px;
  }

  .profile-header {
    flex-direction: column;
    align-items: center;
  }

  .card-body {
    text-align: center;
  }

  .card-img-top {
    width: 70%;
    margin: 0 auto;
  }
}

/* Breakpoint 576px */
@media (max-width: 576px) {
  .ms_style .card {
    padding-top: 15px;
  }

  .profile-header {
    flex-direction: column;
    align-items: center;
  }

  .card-body {
    text-align: center;
  }

  .card-img-top {
    width: 60%;
    margin: 0 auto;
  }
}

/* Breakpoint 450px */
@media (max-width: 450px) {
  .cont-top {
    padding: 5px;
  }

  .profile-photo {
    width: 80px;
    height: 80px;
  }

  .profile-details {
    text-align: center;
  }

  .ms_style .card {
    padding-top: 10px;
  }

  .card-body {
    text-align: center;
  }

  .card-img-top {
    width: 50%;
    margin: 0 auto;
  }
}
</style>
