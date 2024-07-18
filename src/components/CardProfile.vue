<script>


export default {
 
  props: {
    doctor: Object,
  },
}
</script>

<template>
  <div class="row">
    <div class="col-sm-6 mb-3 mb-sm-0">
      <div class="card carddx text-center d-flex align-items-center justify-content-center">
        <div class="card-body">
            <h3 class="title">Inizia il tuo percorso verso una salute migliore oggi!</h3>
          <p class="card-text ">Prenota una consulenza con il Dott. {{ doctor.user.name }} {{ doctor.user.surname }}</p>
          
          <div class="input">
            <input class="input-submit text-light" type="submit" value="Contattami" />
          </div>
        </div>
      </div>
    </div>
    <div class="col-sm-6">
      <div class="card cardsx d-flex align-items-center justify-content-center">
        <div class="card-body text-center">
            <h3 class="title">La tua opinione conta!</h3>
            <p class="card-text">Hai avuto un'esperienza con il Dr. {{ doctor.user.name }} {{ doctor.user.surname }}? Lascia una recensione e aiutaci a migliorare!</p>
            <div class="input">
          <input class="input-submit text-light" type="submit" value="Lascia una recensione"  />
        </div>
        </div>
      </div>
    </div>
  </div>
</template>





<style lang="scss" scoped>
@use"../style/partials/_variables" as*;

.card {
  //position: relative;
  //top: 0px;
  //margin-top: 0;
  //margin-bottom: -145px;
  margin: 50px 0;
  height: 30vh;
}

.carddx {
  border-radius: 10px;
  color: white;
  background-color: transparent;
  background-image:linear-gradient(45deg, #0a369dff, #4472caff, #5e7ce2ff, #92b4f4ff, #cfdee7ff);
  box-shadow: -3px 9px 34px 0 rgba(0, 0, 0, 0.25);
  width: 95%;
}

.card-text {
  text-align: center;
  padding-top: 20px;
}

.input {
  border-radius: 20px;
  background: #70707059;
  padding: 10px 30px;
  width: 70%;
  margin: 0 auto;
  //margin: 23px;

//   .input-email {
//     border: 0;
//     background: #70707000;
//     padding-left: 5px;
//     padding-right: 20px;
//   }
}

.input-submit {
  border: 0;
  background: #70707000;
  color: #707070f2;
  text-align: end;
  padding-left: 20px;
  padding-right: 5px;
  
}


// .button {
//   text-align: center;
//   margin: 20px 0;
// }

.cardsx {
  background-image:linear-gradient(45deg, #0a369dff, #4472caff, #5e7ce2ff, #92b4f4ff, #cfdee7ff);
  border-radius: 10px;
  color: white;
  width: 95%;
  box-shadow: -3px 9px 34px 0 rgba(0, 0, 0, 0.25);
}

.card-body {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>