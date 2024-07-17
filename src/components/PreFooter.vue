<script>
export default {
  data() {
    return {};
  },
};
</script>

<template>
  <div id="carouselExample" class="carousel slide">
    <div class="carousel-inner">
      <div class="ms_icon-color ms_bg1 text-center carousel-item active">
        <div class="w-50">
            <i class="fs-1 fa-solid fa-calendar-check"></i>
            <h3 class="fw-bold py-3">Prenotazione di Appuntamenti Online</h3>
            <p>
              La piattaforma consente agli utenti di prenotare facilmente
              appuntamenti medici online. Gli utenti possono selezionare il medico,
              scegliere la data e l'orario disponibili, e ricevere conferme e
              promemoria via email o SMS, rendendo il processo di prenotazione
              semplice e comodo.
            </p>
        </div>
      </div>
      <div class="ms_bg2 carousel-item">
      </div>
      <div class="ms_bg3 carousel-item">
      </div>
      <div class="ms_bg4 carousel-item">
      </div>
    </div>
    <button
      class="carousel-control-prev"
      type="button"
      data-bs-target="#carouselExample"
      data-bs-slide="prev"
    >
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </button>
    <button
      class="carousel-control-next"
      type="button"
      data-bs-target="#carouselExample"
      data-bs-slide="next"
    >
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </button>
  </div>

  <!-- <div class="ms_bg text-center p-5">
    <div class="container">
      <div class="row">
        <div class="col">
          <i class="fs-1 fa-solid fa-calendar-check"></i>
          <h3 class="fw-bold py-3">Prenotazione di Appuntamenti Online</h3>
          <p>
            La piattaforma consente agli utenti di prenotare facilmente
            appuntamenti medici online. Gli utenti possono selezionare il
            medico, scegliere la data e l'orario disponibili, e ricevere
            conferme e promemoria via email o SMS, rendendo il processo di
            prenotazione semplice e comodo.
          </p>
        </div>
        <div class="col">
          <i class="fs-1 fa-solid fa-user-doctor"></i>
          <h3 class="fw-bold py-3">Consultazioni Mediche Online</h3>
          <p>
            Gli utenti possono accedere a consultazioni mediche online tramite
            videoconferenza, telefono o chat. Questo servizio offre la comodità
            di consultarsi con un medico da casa, ideale per chi ha difficoltà a
            recarsi fisicamente in uno studio medico.
          </p>
        </div>
        <div class="col">
          <i class="fs-1 fa-solid fa-comment-medical"></i>
          <h3 class="fw-bold py-3">Accesso a Feedback e Recensioni</h3>
          <p>
            Gli utenti possono visualizzare feedback e recensioni sui medici
            registrati sulla piattaforma. Questo aiuta gli utenti a fare scelte
            più informate riguardo ai professionisti a cui rivolgersi, basandosi
            sulle esperienze di altri pazienti.
          </p>
        </div>
        <div class="col">
          <i class="fs-1 fa-solid fa-bell"></i>
          <h3 class="fw-bold py-3">Promemoria e Gestione delle Terapie</h3>
          <p>
            Gli utenti possono ricevere promemoria per le terapie e i farmaci
            prescritti tramite notifiche via SMS o email. Questo servizio aiuta
            gli utenti a seguire correttamente le indicazioni mediche e a non
            dimenticare le somministrazioni, migliorando l'aderenza ai
            trattamenti.
          </p>
        </div>
      </div>
    </div>
  </div> -->
</template>

<style scoped lang="scss">
@use "../style/partials/variables" as *;
.ms_bg1 {
    background-image: url(../assets/img/nursing1.jpg);
    background-size: cover;
}

.ms_bg2 {
    background-image: url(../assets/img/nursing2.png);
    background-size: cover;
}

.ms_bg3 {
    background-image: url(../assets/img/nursing3.jpg);
    background-size: cover;
}

.ms_bg4 {
    background-image: url(../assets/img/nursing4.jpg);
    background-size: cover;
}

.ms_icon-color {
    color: $egyptian-blue;
}
</style>
