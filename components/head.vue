<template>
    <div>
        <div class="home-animation-window">
            <div class="window-side"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-center border"></div>
            <div class="window-side right border"></div>
        </div>
        <a class="logo" href="/">gaetan avez.</a>
        <div class="social">
            <a href="https://www.linkedin.com/in/gaetan-avez/" title="Gaëtan Avez - Linkedin"><img src="~/assets/images/linkedin.svg" alt="Linkedin logo"></a>
            <a href="https://dribbble.com/GaetanAvez" title="Gaëtan Avez - Dribbble"><img src="~/assets/images/dribble.svg" alt="Dribbble logo"></a>
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
    }

</style>