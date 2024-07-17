<script>
import axios from "axios";
import { store } from "../store.js";

export default {
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
  <div class="container">
    <div class="row align-items-center ms_style">
      <div class="card mb-3" style="max-width: 1000px">
        <!-- Allargare la card -->
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
                  <template v-if="index > 0">e </template>
                  <strong>{{ specialization.title }}</strong>
                </span>
                <br>
                <span > Tipo di prestazione: </span>
                <span class="text-secondary"><strong>{{ doctor.performance }}</strong></span>
                
              </div>
              <div class="mt-2">
                <p class="m-0">
                  <i class="fa-solid fa-location-dot"></i> {{ doctor.studio_address }}</p>
                <p class="m-0"><i class="fa-solid fa-address-card"></i> {{ doctor.user.email }}</p>
                <p class="m-0"><i class="fa-solid fa-phone"></i> {{ doctor.phone_number }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<style scoped lang="scss">
.ms_style {
  justify-content: center;
  margin-top: 150px;

  .card {
    border: none;
  }
}
.user-picture {
  max-width: 200px; /* Esempio di larghezza massima dell'immagine */
  margin: 0 auto; /* Centrare l'immagine */
}
span {
  font-weight: 900;
  font-style: italic;
}
</style>
