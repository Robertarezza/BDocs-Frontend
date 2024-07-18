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

    .footer-top {
        color: white;
        background-color: $celtic-blue;
        padding: 50px;
        display: flex;
        justify-content: space-around;
        align-items: center;



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
                    padding-left: 0;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    gap: 10px;

                    li {
                        margin-left: 0;
                        list-style-type: none;

                        a {
                            text-decoration: none;
                            color: white;
                            font-size: 1.6rem;
                        }
                    }
                }
            }
        }

        

    .footer-bottom {
        height: 50px;
        background-color: black;
        color: white;
        display: flex;
        justify-content: center;
        align-items: center;

        h4 {
            font-size: .9rem;
        }
    }

    @media screen and (max-width: 992px) {

        .footer-top {
            height: 100%;
            flex-direction: column;

            img {
                height: 40px;
            }
        }
    }

    @media screen and (max-width: 570px) {}

    @media screen and (max-width: 450px) {}
}
</style>