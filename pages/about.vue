<template>
    
    <div class="container">
        <Head />
        <div class="content about">
            <div class="row align-row top">
                <div class="taille-3 gaetan-profile-pic">
                    <div class="pic">
                        <!-- <div class="sub-square square-1"></div>
                        <div class="sub-square square-2"></div>
                        <div class="sub-square square-3"></div> -->
                        <img src="~/assets/images/about_pic.png" alt="">
                    </div>
                </div>
                <div class="taille-2 description">
                    <h1>Hello, my name is <span class="subline">Gaëtan Avez, </span>i’m a french designer based in Paris.  </h1>
                    <div class="txt">
                        I’m looking for a <b>9 months internship</b> in UX/UI design starting February 2020.
                        <br> <br>
                        If you’r interested send me a <u>message</u>
                    </div>
                        <br>
                    <a href="/files/AVEZ_Gaetan_CV_EN.pdf" title="download my resume" target="_blank">My resume <img src="~/assets/images/download_button.svg" alt="download"></a>
                </div>
            </div>
            
            <div class="row skills">
                <h2 class="title">Experience</h2>
                <div class="row taille-3 ">
                    <div class="taille-3 align-row exp-row">
                        <div class="taille-1 align-column">
                            <span class="job-position">Designer</span>
                            <span class="job-description ">UI-UX</span>
                        </div>
                        <div class="taille-1 align-column">
                            <span class="job-locality">BALTAZAR</span>
                            <span class="job-type">Agency</span>
                        </div>
                        <div class="taille-1 align-column">
                            <span class="job-year">2019</span>
                        </div>
                    </div>
                    
                    <div class="taille-3 align-row exp-row">
                        <div class="taille-1 align-column">
                            <span class="job-position">Designer</span>
                            <span class="job-description ">UI-UX</span>
                        </div>
                        <div class="taille-1 align-column">
                            <span class="job-locality">Thibaultrichard.fr</span>
                            <span class="job-type">Portfolio</span>
                        </div>
                        <div class="taille-1 align-column">
                            <span class="job-year">2019</span>
                        </div>
                    </div>

                    <div class="taille-3 align-row exp-row">
                        <div class="taille-1 align-column">
                            <span class="job-position">Designer</span>
                            <span class="job-description ">UI-UX</span>
                        </div>
                        <div class="taille-1 align-column">
                            <span class="job-locality">UniColor</span>
                            <span class="job-type">School Project</span>
                        </div>
                        <div class="taille-1 align-column">
                            <span class="job-year">2019</span>
                        </div>
                    </div>
                

                </div>
            </div>

            <div class="row align-row skills">
                <div class="taille-3">
                    <h2 class="title">Languages</h2>
                    <div class="align-column">
                        <div class="align-row taille-2 lang-row">
                            <div class="taille-1">
                                <span class="lang-type">French</span>
                            </div>
                            <div class="taille-1">
                                <span class="lang-level">Native</span>
                            </div>
                        </div>
                        
                        <div class="align-row taille-2 lang-row">
                            <div class="taille-1">
                                <span class="lang-type">English</span>
                            </div>
                            <div class="taille-1">
                                <span class="lang-level">Fluent</span>
                            </div>
                        </div>

                        <div class="align-row taille-2 lang-row">
                            <div class="taille-1">
                                <span class="lang-type">Spanish</span>
                            </div>
                            <div class="taille-1">
                                <span class="lang-level">Elementary</span>
                            </div>
                        </div>

                    </div>
                </div>
                <div class="taille-2">
                    <h2 class="title">Skills</h2>
                    <div class="taille-2 align-column">
                        <div class="taille-2 skill-row align-column">
                            <span class="skill-title">Design</span>
                            <span class="skill-description">Sketch, Principle, Photoshop, Illustrator</span>
                        </div>

                        <div class="taille-2 skill-row align-column">
                            <span class="skill-title">Web developpment</span>
                            <span class="skill-description">HTML 5, CSS3, JavaScript, PHP</span>
                        </div>

                        <div class="taille-2 skill-row align-column">
                            <span class="skill-title">Photography</span>
                            <span class="skill-description">Lightroom</span>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
import Head from '~/components/Head.vue'
export default {
    head() {
        return {
            title: "Gaetan Avez - About Me"
        };
    }, 
    components:{
        Head
    }
}
</script>

<style>
body{
    padding-top:10%;
}
    .content.about{
        padding: 0 15.5%;;

    }
    .content.about .align-row{
        display: flex;
        flex-direction: row;
    }

    /* descirption part */
    .content.about .top{
        /* background-color: orange;  */
        margin-bottom:65px;
    }
    .content.about .gaetan-profile-pic{


    }
    .content.about .gaetan-profile-pic .pic{
        display: flex;
        justify-content: center;
        position: relative;
    }
    .content.about .gaetan-profile-pic .pic .sub-square{
        position: absolute;
        width: 60%;
        height: 100%;

    }
    .content.about .gaetan-profile-pic .pic .square-1{
        border: 7px solid #473C30;

    }
    .content.about .gaetan-profile-pic .pic .square-2{
        border: 7px solid #726353;

    }
    .content.about .gaetan-profile-pic .pic .square-3{
        border: 7px solid #D7C6B3;

    }
    .content.about .gaetan-profile-pic .pic img{
        width:70%;

    }

    .content.about .description{


    }

    .content.about .description h1{
        color: white;
        font-size: 48px;
        margin-bottom: 15px;
    }
    .content.about .description .txt{
        color:white;
        font-size: 20px;
        font-weight: normal;

    }
    .content.about .description .txt b{
        font-weight: bold;

    }
    .content.about .description .txt u{
        text-decoration: none;
        border-bottom: 1px solid white;
        display: inline-block;
        line-height: 0.85;

    }
    .content.about .description a{
        font-size: 20px;
        color: white;
        margin-top:14px;

    }
    .content.about .description a img{
        width: 22px;
        height: 22px;
        vertical-align: middle;

    }



    /* skills common */
    .content.about .subline{

    }

    .content.about .skills{
        margin-bottom: 66px;
    }

    .content.about .skills .title{
        font-size: 62px;
        color: white;
        margin-top: 0;
        margin-bottom: 26px;
    }

    .content.about .align-column{
        display: flex;
        flex-direction: column;
    }

    .content.about .exp-row{
        margin-bottom: 10px;
    }
    .content.about .lang-row{
        margin-bottom: 10px;
    }
    .content.about .skill-row{
        margin-bottom: 12px;
    }

    /* experience part */
    .content.about .job-position{
        color:white;
        font-size: 22px;
    }
    .content.about .job-description{
        color:#A6A6A6;
        font-size: 16px;
    }
    .content.about .job-locality{
        color:white;
        font-size: 22px;
    }
    .content.about .job-type{
        color:#A6A6A6;
        font-size: 16px;
    }
    .content.about .job-year{
        color:white;
        font-size: 22px;
    }

    /* language part */
    .content.about .lang-type{
        font-size: 22px;
        color:white;
    }
    .content.about .lang-level{
        font-size: 22px;
        color: #A6A6A6;
    }

    /* skills part  */
    .content.about .skill-title{
        font-size: 24px;
        color: white;
    }
    .content.about .skill-description{
        font-size: 22px;
        color: #A6A6A6;
    }
</style>