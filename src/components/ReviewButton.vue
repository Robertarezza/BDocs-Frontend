<template>
    <div>
      <!-- Bottone per aprire il div -->
      <button type="button" class="btn ms_brown_btn" @click="toggleDiv">
        Mostra Recensioni
      </button>
  
      <!-- Div nascosto che si apre al click -->
      <div v-if="showDiv" class="reviews-container">
        <h2>Recensioni</h2>
        <p>Qui verranno visualizzate le recensioni.</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin non justo ac nulla scelerisque gravida. Nulla facilisi. Cras et convallis sapien, vel eleifend est. Sed ultricies ullamcorper magna, at feugiat enim auctor a. Aenean nec sem sit amet massa scelerisque blandit. Suspendisse potenti.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        //per mostrare/nascondere il div
        showDiv: false, 
      };
    },
    methods: {
      toggleDiv() {
        // Cambia lo stato per mostrare/nascondere il div
        this.showDiv = !this.showDiv; 
      },
    },
  };
  </script>
  
  <style scoped>
  .ms_brown_btn {
    background-color: rgba(146, 180, 244, 1);
    color: white;
  }
  .reviews-container {
    margin-top: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  </style>
  