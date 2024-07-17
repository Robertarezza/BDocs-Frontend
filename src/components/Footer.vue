<script>
export default {
    data() {
        return {

        }
    },
}
</script>

<template>
    <footer>
        <div class="footer-top">
            <div>

            </div>

            <div class="contact-us">
                <h3>Contattaci</h3>
                <div class="contacts">
                    <div class="cellphone">
                        <a href="">+(44) 3384893124</a>
                        <a href="">+(44) 2482457890</a>
                    </div>
                    <ul class="social">
                        <li>
                            <a href="">
                                <i class="fa-brands fa-x-twitter"></i>
                            </a>
                        </li>
                        <li>
                            <a href="">
                                <i class="fa-brands fa-facebook"></i>
                            </a>
                        </li>
                        <li>
                            <a href="">
                                <i class="fa-brands fa-instagram"></i>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <div class="footer-bottom">
            <h4>
                @B-Doctors since 2024
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
        padding: 30px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .contact-us {
            width: 30%;
            display: flex;
            flex-direction: column;
            align-items: center;
            
            .contacts {

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
            font-size: .8rem;
        }
    }
}
</style>