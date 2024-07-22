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
        // Chiamata API
        submitForm() {
            console.log(this.formData);
            axios
                .post(`http://127.0.0.1:8000/api/ratings`, this.formData)
                .then((resp) => {
                    // console.log(resp);
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
        }
    },
};
</script>

<template>
    <div>
        <!-- Bottone per aprire il Modale -->
        <button type="button" class="btn ms_brown_btn" @click="showModal = true">
            Lascia un voto
        </button>

<!-- Modale -->
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

                    <!-- Form del Modale -->
                    <div class="modal-body">
                        <form @submit.prevent="submitForm">

                            <!-- ID del dottore di riferimento -->
                            <input type="hidden" v-model="formData.doctor_id" />

                            <!-- Nome -->
                            <div class="mb-3">
                                <label class="form-label text-secondary" for="rating_id">Inserisci il tuo voto*</label>
                                <select id="rating_id" class="form-select" v-model="formData.rating_id">
                                    <!-- <option value="">Tutti i voti</option> -->
                                    <option value="1">1</option>
                                    <option value="2">2</option>
                                    <option value="3">3</option>
                                    <option value="4">4</option>
                                    <option value="5">5</option>
                                </select>
                            </div>

                            <div class="mt-1 text-muted">
                                <small>* Campi obbligatori</small>
                            </div>

                            <!-- Submit -->
                            <div class="d-flex gap-2 mt-2">
                                <button type="submit" class="btn btn-primary">Invia</button>
                                <button type="button" class="btn btn-danger" @click="closeModal" aria-label="Close">
                                    Annulla
                                </button>
                            </div>
                        </form>
                    </div>
                    <!-- /Form del Modale -->
                </div>
            </div>
        </div>
        <!-- /Modale -->    </div>
</template>

<style lang="scss" scoped>
.ms_brown_btn {
    background-color: rgba(146, 180, 244, 1);
    color: white;
}



@media screen and (max-width: 768px) {

    button {
        font-size: 12px;
        margin: 0;
        padding: 2px 10px;
    }

}

</style>