<script>
export default {
    props: {
        doctor: Object,
    },
    mounted() {
        window.addEventListener('scroll', this.handleScroll);
        this.$nextTick(() => {
            this.handleScroll();
        });
    },
    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        handleScroll() {
            const cards = document.querySelectorAll('.fade-in');
            const windowHeight = window.innerHeight;

            cards.forEach(card => {
                const rect = card.getBoundingClientRect();
                if (rect.top < windowHeight && rect.bottom > 200) {
                    card.classList.add('visible');
                } else {
                    card.classList.remove('visible');
                }
            });
        }
    }
}
</script>

<template>
    <div class="row">
        <div class="col-sm-6 mb-3 mb-sm-0">
            <div class="card carddx text-center d-flex align-items-center justify-content-center fade-in">
                <div class="card-body">
                    <h3 class="title">Inizia il tuo percorso verso una salute migliore oggi!</h3>
                    <p class="card-text">Prenota una consulenza con il Dott. {{ doctor.user.name }} {{ doctor.user.surname }}</p>
                    <div class="input">
                        <input class="input-submit text-light" type="submit" value="Contattami" />
                    </div>
                </div>
            </div>
        </div>
        <div class="col-sm-6">
            <div class="card cardsx d-flex align-items-center justify-content-center fade-in">
                <div class="card-body text-center">
                    <h3 class="title">La tua opinione conta!</h3>
                    <p class="card-text">Hai avuto un'esperienza con il Dr. {{ doctor.user.name }} {{ doctor.user.surname }}? Lascia una recensione e aiutaci a migliorare!</p>
                    <div class="input">
                        <input class="input-submit text-light" type="submit" value="Lascia una recensione" />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@use "../style/partials/_variables" as *;

// Animazione hover P.CArd
.card {
    margin: 50px 0;
    height: 30vh;
    transition: transform 0.3s ease, box-shadow 0.3s ease; 
}

.carddx, .cardsx {
    border-radius: 10px;
    color: white;
    background-image: linear-gradient(315deg, #0a369dff, #4472caff, #5e7ce2ff, #92b4f4ff, #cfdee7ff);
    box-shadow: -3px 9px 34px 0 rgba(0, 0, 0, 0.25);
    width: 95%;
}

// Solleva la card
.card:hover {
  transform: translateY(-10px); 
    box-shadow: -3px 15px 40px 0 rgba(0, 0, 0, 0.3); 
}


.card-text {
    text-align: center;
    padding-top: 20px;
}

.input {
    border-radius: 20px;
    background:  rgba(146, 180, 244, 1);
    padding: 10px 30px;
    width: 45%;
    margin: 0 auto;
}

.input-submit {
    border: 0;
    background: #70707000;
    color: #707070f2;
    text-align: end;
    padding-left: 20px;
    padding-right: 5px;
}

.card-body {
    display: flex;
    flex-direction: column;
    justify-content: center;
}

/* Animazione fade-in CUBIC ;) */
.fade-in {
    opacity: 0;
    transition: opacity 1s cubic-bezier(0.25, 0.1, 0.25, 1);
}

.fade-in.visible {
    opacity: 1;
}
</style>
