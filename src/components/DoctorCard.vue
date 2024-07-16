<script>
import { store } from "../store.js";

export default {
  props: {
    doctor: Object,
  },
  data() {
    return {
      store,
    };
  },
};
</script>

<template>
  <div class="card-client">
    <div class="user-picture">
      <img
        :src="
          doctor.photo
            ? `${store.imageUrl}/${doctor.photo}`
            : `https://t3.ftcdn.net/jpg/02/48/42/64/360_F_248426448_NVKLywWqArG2ADUxDq6QprtIzsF82dMF.jpg`
        "
        class="card-img-top"
        alt="Doctor Photo"
      />
    </div>

    <h5 class="name-client">{{ doctor.user.name }} {{ doctor.user.surname }}</h5>

    <span v-for="specialization in doctor.specializations" :key="specialization.id">
      <strong>{{ specialization.title }},</strong>
    </span>
    <p>E-mail: {{ doctor.user.email }}</p>

    <!-- Card Supplemento -->
    <div class="card-supp ">
    <a href="" title=""><i class="fa-solid fa-location-dot"> </i></a>
      
      <!-- <p class="card-text">Indirizzo:{{ doctor.studio_address }} </p> -->
    
      <a href="" title=""><i class="fa-solid fa-phone"></i></a>
      <a href="" title=""><i class="fa-solid fa-address-card"></i></a>
      
      <!-- <p class="card-text">Telefono: {{ doctor.phone_number }}</p> -->
      <!-- <p class="card-text">Prestazioni: {{ doctor.performance }}</p> -->
    </div>
  </div>
</template>

<style scoped lang="scss">
@use "../style/partials/variables" as *;

.card-client {
 // background: rgba(207, 222, 231, 1);
  margin-bottom: 40px;
  width: 22rem;
  height: 27rem;
  padding: 25px;
  border: 4px solid rgba(94, 124, 226, 1);
  border-bottom: none;
  box-shadow: 0 6px 10px rgba(207, 222, 231, 1);
  border-radius: 10px 10px 0 0; /* Arrotonda solo gli angoli superiori */
  text-align: center;
  color: black;
  font-family: "Poppins", sans-serif;
  position: relative; /* Necessario per posizionamento relativo al genitore */
}

.card-client:hover {
  transform: translateY(-10px);
}

.user-picture {
  overflow: hidden;
  object-fit: cover;
  width: 10rem;
  height: 10rem;
  border: 2px solid rgba(94, 124, 226, 1);
  border-radius: 999px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
}

.user-picture svg {
  width: 2.5rem;
  fill: currentColor;
}

.name-client {
  margin: 0;
  margin-top: 20px;
  font-weight: 600;
  font-size: 18px;
}

.name-client span {
  display: block;
  font-weight: 200;
  font-size: 16px;
}

.card-supp {
  background-color: white;
  padding: 10px;
  position: absolute;
  bottom: -20px; /* Sovrapponi la parte superiore di .card-client */
  left: 0;
  right: 0;
  margin: auto;
  height: 7rem;
  width: calc(100% - 40px); /* Larghezza meno il padding */
  border: 2px solid rgba(94, 124, 226, 1);
  border-bottom: none; /* Rimuovi il bordo superiore di .card-supp */
  border-radius: 10px 10px 0 0; /* Arrotonda solo gli angoli superiori */
  text-align: left; /* Allinea il testo a sinistra */
  display: flex;
  justify-content: space-around;
    align-items: center;

  .fa-solid {
    font-size: 2rem;
  
  }
}

.card-supp p {
  margin-bottom: 10px;
}

.card-text ul {
  padding-left: 20px;
  list-style: disc;
}
</style>