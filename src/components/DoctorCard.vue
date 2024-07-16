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
  <div class="card h-100">
    <img
      :src="
        doctor.photo
          ? `${store.imageUrl}/${doctor.photo}`
          : `https://t3.ftcdn.net/jpg/02/48/42/64/360_F_248426448_NVKLywWqArG2ADUxDq6QprtIzsF82dMF.jpg`
      "
      class="card-img-top"
      alt="Doctor Photo"
      style="object-fit: cover; height: 200px"
    />
    <div class="card-body">
      <h5 class="card-title">{{ doctor.user.name }} {{ doctor.user.surname }}</h5>
      <p class="card-text">E-mail: {{ doctor.user.email }}</p>
      <p class="card-text">Indirizzo: {{ doctor.studio_address }}</p>
      <p class="card-text">Telefono: {{ doctor.phone_number }}</p>
      <p class="card-text">Prestazioni: {{ doctor.performance }}</p>
      <p>Specializzazioni:</p>
      <ul class="card-text">
        <li v-for="specialization in doctor.specializations" :key="specialization.id">
          {{ specialization.title }}
        </li>
      </ul>
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

.card-img-top {
  object-fit: cover;
  height: 200px;
}

.card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
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
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
