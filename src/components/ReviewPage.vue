<script>
import axios from "axios";

export default {
    props: {
        doctor: Number,
    },
    data() {
        return {
            showModal: false,
            formData: {
                doctor_id: this.doctor,
                guest_name: "",
                guest_mail: "",
                review: "",
            },
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
                .post(`http://127.0.0.1:8000/api/reviews`, this.formData)
                .then((resp) => {
                    // console.log(resp);
                    if(resp.data.success) {
                        this.clearFields();
                        this.closeModal();
                    }
                })
                .catch((error) => {
                    console.error(error.response.data);
                });
        },
        clearFields() {
            this.formData.guest_name = ""; 
            this.formData.guest_mail = ""; 
            this.formData.review = ""; 
        }
    },
};
</script>

<template>
    <div>
        <!-- Bottone per aprire il Modale -->
        <button type="button" class="btn ms_brown_btn" @click="showModal = true">
            Lascia una recensione
        </button>

        <!-- Modale -->
        <div v-if="showModal" class="modal fade show" tabindex="-1" role="dialog"
            aria-labelledby="contactHostModalLabel" style="display: block; background: rgba(0, 0, 0, 0.5)"
            @click.self="closeModal">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title text-secondary" id="contactHostModalLabel">
                            Lascia una recensione
                        </h5>
                    </div>

                    <!-- Form del Modale -->

                    <div class="modal-body">
                        <form @submit.prevent="submitForm">

                            <!-- ID del dottore di riferimento -->
                            <input type="hidden" v-model="formData.doctor" />

                            <!-- Nome -->
                            <div class="form-group" style="text-align: justify">
                                <label class="my-1 text-secondary " for="guest_name">Inserisci il tuo nome*</label>
                                <input type="text" class="form-control" id="guest_name" v-model="formData.guest_name"
                                    required />
                            </div>
                            <!-- /Nome -->

                            <!-- Email -->
                            <div class="form-group " style="text-align: justify">
                                <label class="my-1 text-secondary" for="guest_mail">Inserisci la tua e-mail *</label>
                                <input type="email" class="form-control" id="guest_mail" v-model="formData.guest_mail"
                                    required />
                            </div>
                            <!-- /Email -->

                            <!-- Messaggio -->
                            <div class="form-group" style="text-align: justify">
                                <label class="my-1 text-secondary" for="review">Lascia la tua recensione *</label>
                                <textarea class="form-control" id="review" v-model="formData.review" rows="5"
                                    required></textarea>
                            </div>
                            <!-- /Messaggio -->

                            <div class="mt-1 text-muted" style="text-align: justify">
                                <small>* Campi obbligatori</small>
                            </div>

                            <!-- Submit -->
                            <div class="d-flex gap-2 mt-2">
                                <button type="submit" class="btn btn-primary">Invia</button>
                                <button type="button" class="btn btn-danger" @click="closeModal" aria-label="Close">
                                    Annulla
                                </button>
                            </div>
                            <!-- /Submit -->
                        </form>
                    </div>
                    <!-- /Form del Modale -->
                </div>
            </div>
        </div>
        <!-- /Modale -->
    </div>
</template>

<style lang="scss" scoped>
.ms_brown_btn {
    background-color: rgba(146, 180, 244, 1);
    color: white;
}
</style>