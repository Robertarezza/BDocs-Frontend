<script>
export default {
    data() {
        return {

        }
    },
}
</script>

<template>
    <footer id="footer">
        <div class="footer-top">
            <div class="form-contact">
                <h4>Aiutaci a migliorare la tua esperienza</h4>

                <form action="">
                    <input type="text" id="name" placeholder="Inserisci il tuo nome" aria-label="name">

                    <input type="email" id="email" placeholder="Inserisci una mail valida" aria-label="email">

                    <textarea id="message" aria-label="message" placeholder="Come possiamo migliorare?"></textarea>

                    <div id="submit">
                        <button type="submit">Invia</button>
                    </div>
                </form>
            </div>

            <div class="contact-us">
                <img src="../assets/img/logo.png" alt="">
                <h3>Contattaci</h3>
                <div class="contacts">
                    <div class="cellphone">
                        <a href="">+(44) 3384893124</a>
                        <a href="">+(44) 2482457890</a>
                    </div>
                    <ul class="social">
                        <li>
                            <a href="http://127.0.0.1:8000/" class="btn ">
                               
                            </a>
                        </li>
                        <li>
                            <a href="https://www.facebook.com/simone.bonvecchio/?locale=it_IT">
                                <i class="fa-brands fa-facebook"></i>
                            </a>
                        </li>
                        <li>
                            <a href="https://www.instagram.com/">
                                <i class="fa-brands fa-instagram"></i>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <div class="footer-bottom">
            <h4>
                © 2024 B-Doctors. All Rights Reserved.
            </h4>
        </div>
    </footer>
</template>

<style scoped lang="scss">
@use "../style/partials/variables" as *;

footer {
    width: 100%;
    height: 600px;

    .footer-top {
        color: white;
        height: 80%;
        background-color: $celtic-blue;
        padding: 50px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .form-contact {
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            width: 50%;
            padding: 20px;
            background-color: white;
            border-radius: 10px;

            h4 {
                text-align: left;
                color: $celtic-blue;
            }

            input {
                margin-top: 20px;
                border: 0;
                border-bottom: 1px solid $celtic-blue;
                width: 100%;
                height: 30px;
                padding: 5px;
                background-color: transparent;

                :focus {
                    border: 0;
                    background-color: $celtic-blue;
                }
            }

            ::placeholder {
                color: $celtic-blue;
                font-size: .7rem;
            }

            textarea {
                padding: 5px;
                margin-top: 20px;
                border: 0;
                border-bottom: 1px solid $celtic-blue;
                width: 100%;
                outline: none;
                resize: none;
            }


            #submit {
                width: 100%;
                text-align: left;

                button {
                    margin-right: 370px;
                    margin-top: 10px;
                    padding: 6px 10px;
                    color: white;
                    border: 1px solid $celtic-blue;
                    border-radius: 10px;
                    background-color: $celtic-blue;
                }
            }
        }

        .contact-us {
            width: 30%;
            display: flex;
            flex-direction: column;
            align-items: start;

            img {
                height: 40px;
                margin-bottom: 20px;
            }

            .contacts {
                margin-top: 20px;

                .cellphone {
                    display: flex;
                    flex-direction: column;
                    justify-content: space-around;
                    margin-bottom: 40px;

                    a {
                        text-decoration: none;
                        color: white;
                    }
                }

                .social {
                    display: flex;
                    justify-content: space-around;
                    padding-left: 0;

                    li {
                        list-style-type: none;

                        a {
                            color: white;
                            font-size: 1.6rem;
                        }
                    }
                }
            }
        }
    }

    .footer-bottom {
        height: 20%;
        background-color: black;
        color: white;
        display: flex;
        justify-content: center;
        align-items: center;

        h4 {
            font-size: .9rem;
        }
    }
}
</style>