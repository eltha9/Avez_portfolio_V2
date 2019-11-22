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
                    <a class="dirbbble-responsive" href="https://dribbble.com/GaetanAvez" title="Gaëtan Avez - Dribbble" target="_blank"><img src="~/assets/images/dribble.svg" alt="Dribbble logo"></a>
                    <a href="https://www.linkedin.com/in/gaetan-avez/" title="Gaëtan Avez - Linkedin" target="_blank"><img src="~/assets/images/linkedin.svg" alt="Linkedin logo"></a>
                </div>
                <a class="logo" href="/">gaetan avez.</a>
                <button class="burger-menu">
                    <div class="top"></div>
                    <div class="middle"></div>
                    <div class="bottom"></div>
                </button>
            </div>
        </div>
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
            padding-top:2vw; 

        }

        .responsive-menu .responsive-menu-header {
            display: flex;
            flex-direction: row;
            justify-content: space-around;
            align-items: center;
            width: 100%;
        }
            .responsive-menu .responsive-menu-header .responsive-socials{
                display: flex;
                flex-direction: row;
            }
                .responsive-menu .responsive-menu-header .responsive-socials a{
                    display: block;
                    width: 10vw;
                    height: 10vw;
                    background-color: orange;
                }
                    .responsive-menu .responsive-menu-header .responsive-socials a img{
                        width: 100%;
                        height: 100%;
                    }
                .responsive-menu .responsive-menu-header .responsive-socials a.dribbble-responsive{

                }
            .responsive-menu .responsive-menu-header a.logo{
                display: block;
                font-size: 2rem;
            }
            .responsive-menu .responsive-menu-header button.burger-menu{
                width: 10vw;
                height: 10vw;
                background-color: red;
            }
                .responsive-menu .responsive-menu-header button.burger-menu div.top{

                }
                .responsive-menu .responsive-menu-header button.burger-menu div.middle{

                }
                .responsive-menu .responsive-menu-header button.burger-menu div.bottom{

                }

    }

</style>