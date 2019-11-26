<template>
    <div class="menu-vue">
        <!-- <div class="home-animation-window">
            <div class="window-side"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-side right border"></div>
        </div> -->
        <a class="logo" href="/">gaetan avez.</a>
        <div class="social">
            <a class="linkedin" href="https://www.linkedin.com/in/gaetan-avez/" title="Gaëtan Avez - Linkedin" target="_blank"><img src="~/assets/images/linkedin.svg" alt="Linkedin logo"></a>
            <a href="https://dribbble.com/GaetanAvez" title="Gaëtan Avez - Dribbble" target="_blank"><img src="~/assets/images/dribble.svg" alt="Dribbble logo"></a>
        </div>
        <div class="navigation align-row">

                <div class="taille-2 nav-opt"></div>
                <div class="taille-1 nav-opt">
                    <a  href="/about">About me</a>
                </div>
                <div class="taille-1 nav-opt">
                    <a  href="/">Project</a>
                </div>
                <div class="taille-1 nav-opt">
                    <a  href="/contact">Contact</a>
                </div>

        </div>
        <div class="responsive-menu">
            <div class="responsive-menu-header">
                <div class="responsive-socials">
                    <a class="dirbbble-responsive" href="https://dribbble.com/GaetanAvez" title="Gaëtan Avez - Dribbble" target="_blank"><img src="~/assets/images/dribble.svg" alt="Dribbble logo" style="margin-right: 0.6rem;"></a>
                    <a href="https://www.linkedin.com/in/gaetan-avez/" title="Gaëtan Avez - Linkedin" target="_blank"><img src="~/assets/images/linkedin.svg" alt="Linkedin logo"></a>
                </div>
                <a class="responsive-logo" href="/">gaetan avez.</a>
                <button class="burger-menu">
                    <img src="~/assets/images/burger.svg" alt="">
                </button>
            </div>
            <div class="responsive-menu-content">
                <div class="responsive-link">
                    <a href="/about">About Me</a>
                    <a href="/">Projects </a>
                    <a href="/contact">Contact</a>
                </div>
            </div>
        </div>
        <client-only>
            <script>
                //responsive
                const button = document.querySelector('button.burger-menu')
                const menu_content = document.querySelector('.responsive-menu-content')
                let menu_state = false
                button.addEventListener('click', ()=>{
                    if(!menu_state){
                        menu_state = true
                        menu_content.style.left = '0%'
                    }else if(menu_state){
                        menu_state = false
                        menu_content.style.left = '-100%'
                    }
                })


                let burger_animation = ()=>{
                    
                }
            </script>
        </client-only>
    </div>
</template>

<style>
    .align-row{
        display: flex;
        flex-direction: row;
    }
    .navigation{
        /* width: 100vw; */
        width: calc(1vw * 13.8 *5);
        height: 20vh;
        padding: 0 15.5%;
        position: absolute;
        top:0;
        left:0;
        z-index: 40;

    }
    .navigation .nav-opt{
        padding-top: 40px;
        text-align: left;
    }

    .navigation a{
        color: white;
        font-family: Arial;
        font-style: normal;
        font-weight: normal;
        font-size: 16px;
        line-height: 21px;
        mix-blend-mode: difference;
    }
    .responsive-menu{
        display: none;
    }
    
    @media screen and (max-width: 1024px) {
        body{
            overflow-x: hidden;
            width: 100vw;
        }
        .container{
            position: relative;

        }

        .menu-vue *:not(.responsive-menu){
            display: none;
        }
        .menu-vue{
            position: absolute;

            top:0;
            left: 0;
            z-index: 400;
        }

        .responsive-menu{
            display: block;
            width: 100vw;

            background-color: black;
            position: relative;
        }

        .responsive-menu .responsive-menu-header {
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            align-items: center;
            width: 100vw;
            padding-top: 1.5rem;
            z-index: 300;

            position: absolute;
            top:0;
            left:0;
        }
            .responsive-menu .responsive-menu-header .responsive-socials{
                display: flex;
                flex-direction: row;
                padding-left: 0.9rem;
            }
                .responsive-menu .responsive-menu-header .responsive-socials a{
                    display: block;

                    height: 1rem;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                }
                    .responsive-menu .responsive-menu-header .responsive-socials a img{
                        display: block;

                        height: 1rem;
                        margin: 0;
                    }
                .responsive-menu .responsive-menu-header .responsive-socials a.dribbble-responsive{
                    margin-right: 0.6rem;
                }
            .responsive-menu .responsive-menu-header a.responsive-logo{
                display: block;
                font-size: 1rem;

                text-transform: uppercase;
                color: white;
                text-decoration: none;
            }
            .responsive-menu .responsive-menu-header button.burger-menu{
                display: block;

                padding: 0;
                border: none;
                padding-right: 0.9rem;
                display: flex;
                justify-content: center;
                align-items: center;
                background-color: transparent;

                outline: none;
            }
                .responsive-menu .responsive-menu-header button.burger-menu img{
                    display: block;
                    height: 1rem;
                }

            .responsive-menu-content{
                display: block !important;
                position: absolute;   
                top:0;
                left:-100%;
                width: 100vw;
                height: 100vh;
                background-color: black;
                z-index: 200;
                will-change: left;
                transition : left 0.3s ease-out;
            }
                .responsive-menu-content .responsive-link{
                    display: block;
                    height: 100%;
                    display: flex;
                    flex-direction: column;
                    justify-content: space-evenly;
                    z-index: 200;

                    text-align: center;
                    
                }
                    .responsive-menu-content .responsive-link a{
                        display: block ;

                        color: white;
                        font-size: 1.5rem;
                        text-decoration: none;
                    }

    }

</style>