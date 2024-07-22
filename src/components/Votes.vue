<script>
import axios from "axios";
import { store } from "../store";

export default {
    props: {
        doctor: Number,
    },
    data() {
        return {
            showModal: false,
            formData: {
                doctor_id: this.doctor,
                rating_id: 0,
            },
            store,
        };
    },
    methods: {
        closeModal() {
            this.showModal = false;
        },
        submitForm() {
            console.log(this.formData);
            axios
                .post(`http://127.0.0.1:8000/api/ratings`, this.formData)
                .then((resp) => {
                    if (resp.data.success) {
                        this.clearFields();
                        this.closeModal();
                        this.store.successMessage = true;
                        setTimeout(() => {
                            this.store.successMessage = false;
                        }, 3000);
                    }
                })
                .catch((error) => {
                    console.error(error.response.data);
                });
        },
        clearFields() {
            this.formData.rating_id = 0;
        },
        // Metodo per impostare la valutazione cliccando sulle stelle
        setRating(rating) { 
            this.formData.rating_id = rating;
        },
        // Metodo per calcolare la media delle valutazioni
        getAverageRating(ratings) { 
            if (!ratings.length) return 0;
            const sum = ratings.reduce((acc, rating) => acc + rating, 0);
            return (sum / ratings.length).toFixed(2);
        }
    },
};
</script>


<template>
    <div>
        <button type="button" class="btn ms_brown_btn" @click="showModal = true">
            Lascia un voto
        </button>

        <div v-if="showModal" class="modal fade show" tabindex="-1" role="dialog"
            aria-labelledby="contactHostModalLabel" style="display: block; background: rgba(0, 0, 0, 0.5)"
            @click.self="closeModal">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title text-secondary" id="contactHostModalLabel">
                            Lascia un voto
                        </h5>
                        <button type="button" class="btn-close" @click="closeModal" aria-label="Close"></button>
                    </div>

                    <div class="modal-body">
                        <form @submit.prevent="submitForm">
                            <input type="hidden" v-model="formData.doctor_id" />
                            <div class="mb-3">
                                <label class="form-label text-secondary" for="rating_id">Inserisci il tuo voto*</label>
                                <!-- Sezione per la valutazione con stelle -->
                                <div class="star-rating"> 
                                    <i v-for="star in 5" :key="star" 
                                       :class="['fa-star', star <= formData.rating_id ? 'fas' : 'far']" 
                                       @click="setRating(star)"></i> <!-- Aggiunge/stacca stelle in base al rating -->
                                </div>
                                <!-- Sezione per la valutazione con stelle -->
                            </div>
                            <div class="mt-1 text-muted">
                                <small>* Campi obbligatori</small>
                            </div>
                            <div class="d-flex gap-2 mt-2">
                                <button type="submit" class="btn btn-primary">Invia</button>
                                <button type="button" class="btn btn-danger" @click="closeModal" aria-label="Close">
                                    Annulla
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<style lang="scss" scoped>
.ms_brown_btn {
    background-color: rgba(146, 180, 244, 1);
    color: white;
}

// Un po di tile per le stelle 
.star-rating { 
    font-size: 1.5rem;
    color: gold;
    cursor: pointer;
}

.star-rating .fa-star {
    margin: 0 0.1rem;
}

@media screen and (max-width: 768px) {
    button {
        font-size: 12px;
        margin: 0;
        padding: 2px 10px;
    }
}
</style>
