<script>
import { RouterLink } from 'vue-router';

export default {
  data() {
    return {
    }
  },
}
</script>

<template>
  <header class="bg-celtic-blue fixed-top">
    <nav class="container h-100">
      <ul class="d-flex justify-content-between align-items-center h-100 list-unstyled mb-0">
        <li class="box-img">
          <router-link :to="{ name: 'home' }">
            <img src="../assets/img/logo-1.png" alt="logo B-Doctors" class="img-fluid" />
          </router-link>
        </li>
        <li id="title">
          <a href="#footer" class="text-white text-decoration-none">Contattaci</a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style scoped lang="scss">
@use "../style/partials/variables" as *;

header {
  height: 100px;
  background-color: $celtic-blue;
  z-index: 9999;
}

.box-img img {
  max-width: 200px;
}

#title {
  list-style-type: none;

  a {
    text-decoration: none;
    color: white;
  }
}

@media (max-width: 768px) {
  header {
    height: 100px;
  }

  .box-img img {
    max-width: 150px;
  }

  #title a {
    font-size: 1rem; 
  }
}

@media (max-width: 576px) {
  header {
    height: 100px; 
  }

  .box-img img {
    max-width: 100px; 
  }

  #title a {
    font-size: 0.8rem; 
  }
}
</style>
