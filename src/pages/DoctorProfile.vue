<script>
import axios from "axios"; 
import { store } from '../store.js'; 


export default {

    data() {
        return {
            doctor: null,
            store,
        };
    },

    created() {
        const id = this.$route.params.id;
        axios.get(`${store.apiBaseURL}/api/doctors/${id}`)
            .then((resp) => {
                console.log(  resp );
                this.doctor = resp.data.results;
                console.log(  this.doctor );
            })
            .catch(error => {
                console.error('Error fetching doctors:', error); 
            });
    },
};
</script>

<template>
    <div>
      <h1>{{ doctor.user.name }} {{ doctor.user.surname }}</h1>
      <p>Email: {{ doctor.user.email }}</p>
      <p>Telefono: {{ doctor.phone_number }}</p>
      <p>Indirizzo studio: {{ doctor.studio_address }}</p>
      <p>Specializzazioni:</p>
      <ul>
        <li v-for="specialization in doctor.specializations" :key="specialization.id">
          {{ specialization.title }}
        </li>
      </ul>
     
    </div>
  </template>

<style scoped lang="scss">
</style>