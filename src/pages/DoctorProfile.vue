<script>
import axios from "axios";
import { store } from "../store.js";
import CardProfile from "../components/CardProfile.vue";
import PreFooter from "../components/PreFooter.vue";
import Review from "../components/Review.vue";
import Message from "../components/Message.vue";

export default {
  components: {
    CardProfile,
    PreFooter,
    Review,
    Message,
  },

  data() {
    return {
      doctor: null,
      store,
    };
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
  },
};
</script>

<template>
  <div class="container-fluid cont-top">
    <div class="row align-items-center ms_style">
      <div class="card mb-3" style="max-width: 1000px">
        <div class="row g-0">
          <div class="col-md-4">
            <img
              :src="
                doctor.photo
                  ? `${store.imageUrl}/${doctor.photo}`
                  : `https://t3.ftcdn.net/jpg/02/48/42/64/360_F_248426448_NVKLywWqArG2ADUxDq6QprtIzsF82dMF.jpg`
              "
              class="card-img-top"
              alt="Doctor Photo"
              style="max-width: 100%"
            />
          </div>
          <div class="col-md-8 align-content-center">
            <div class="card-body">
              <h1>{{ doctor.user.name }} {{ doctor.user.surname }}</h1>
              <span>Specializzazione </span>
              <div class="d-inline">
                <span
                  class="text-secondary"
                  v-for="(specialization, index) in doctor.specializations"
                  :key="specialization.id"
                >
                  <template v-if="index > 0"> e </template>
                  <strong>{{ specialization.title }}</strong>
                </span>
                <br />
                <span> Tipo di prestazione: </span>
                <span class="text-secondary"
                  ><strong>{{ doctor.performance }}</strong></span
                >
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
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="alert alert-success" v-if="store.successMessage">
    Il tuo messaggio è stato inviato con successo
  </div>
  <div class="container cont-card">
    <CardProfile :doctor="doctor" />
  </div>

  <div class="d-none">
    <Review :doctor="doctor.user.id" />
  </div>
  <div class="d-none">
    <Message :doctor="doctor.user.id" />
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
