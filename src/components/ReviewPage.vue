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
                    console.log(resp);
                    this.closeModal();
                })
                .catch((error) => {
                    console.error(error.response.data);
                });
        },
    },
};
</script>

<template>
    <div>
        <!-- Bottone per aprire il Modale -->
        <button type="button" class="btn ms_brown_btn" @click="showModal = true">
            Contatta il medico
        </button>

        <!-- Modale -->
        <div v-if="showModal" class="modal fade show" tabindex="-1" role="dialog"
            aria-labelledby="contactHostModalLabel" style="display: block; background: rgba(0, 0, 0, 0.5)"
            @click.self="closeModal">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="contactHostModalLabel">
                            Contatta il medico
                        </h5>
                    </div>

                    <!-- Form del Modale -->

                    <div class="modal-body">
                        <form @submit.prevent="submitForm">

                            <!-- ID del dottore di riferimento -->
                            <input type="hidden" v-model="formData.doctor" />

                            <!-- Nome-Cognome -->
                            <div class="form-group">
                                <label class="my-1" for="guest_name">Nome*</label>
                                <input type="text" class="form-control" id="guest_name" v-model="formData.guest_name"
                                    required />
                            </div>
                            <!-- /Nome-Cognome -->

                            <!-- Email -->
                            <div class="form-group">
                                <label class="my-1" for="guest_mail">Email *</label>
                                <input type="email" class="form-control" id="guest_mail" v-model="formData.guest_mail"
                                    required />
                            </div>
                            <!-- /Email -->

                            <!-- Messaggio -->
                            <div class="form-group">
                                <label class="my-1" for="review">Recensione *</label>
                                <textarea class="form-control" id="review" v-model="formData.review" rows="5"
                                    required></textarea>
                            </div>
                            <!-- /Messaggio -->

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
    background-color: #705d3f;
    border: 1px solid #705d3f;
    color: white;

    &:hover {
        background-color: #f8f2eb;
        transition: all 0.7s;
        color: black;
        border: 1px solid #f8f2eb;
    }
}
</style>