<script>
import axios from "axios";
import { store } from '../store.js';
import DoctorCard from "../components/DoctorCard.vue";

export default {
    components : {
        DoctorCard,
    },

  data() {
    return {
      doctor: null,
      store,
      
    };
  },

  created() {
    axios.get(`${this.store.apiBaseURL}/api/doctors`)
      .then((resp) => {
        console.log(resp.data.results);
        this.doctor = resp.data.results;
        console.log(this.doctor);
      })
      .catch(error => {
        console.error('Error fetching doctors:', error);
      });
  },
};
</script>


<template>
    <div class="container mt-5 mb-5">
      <h1 class="text-center mb-3">I nostri Dottori</h1>
      <div v-if="doctor">
        <div class="row row-cols-1 row-cols-md-3 g-3"> 
          <div class="col" v-for="doctor in doctor" :key="doctor.id">
            <DoctorCard :doctor="doctor" />
          </div>
        </div>
      </div>
      <div v-else>
        <div class="loader">
          <span class="loader-text">loading</span>
          <span class="load"></span>
        </div>
      </div>
    </div>
  </template>
  
  

  <style scoped lang="scss">
@use "../style/partials/variables" as *;

.container {
  min-height: 100vh;
  background: $gradient-top;
  padding-top: 50px;
  padding-bottom: 50px;
}

.card {
  margin-bottom: 1rem;
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
</style>

