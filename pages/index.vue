<template>
  <div class="container">
    <Head />
    
    <div class="content index align-row">
        <div class="left-bloc taille-sup-left"></div>

        <div class="taille-5" style="padding-top: 10%; height:100%;">
            <div class="central-bloc taille-5">
                <div style="position: absolute; right:0; bottom:0;">
                    <div style="position:relative">
                        <a  href="" class="project-title">{{projects.project_title}}</a>
                        <div class="big-diapo taille-5">
                            <div class="slider" style="transform: translateX(0);">
                                <div class="slide" v-for="item in projects" style="display:flex;flex-direction:row">
                                    <img :src="item.project_img" alt="" style="margin-right:10vw;">
                                    <img :src="item.project_img_responsive" class="repsonsive_image" style="display:none" alt="" >

                                    <!-- <div class="space" style="width:10vw; height:100%"></div> -->
                                </div>
                            </div>
                        </div>

                        <div class="dots">
                            <div class="dot" v-for="item in projects"></div>
                        </div>

                        <div class="scroll-to-see taille-1">
                            scroll to see more
                            <img src="~/assets/images/project_button.svg" alt="">
                        </div>

                        <div class="state">
                            01
                        </div>
                    </div>
                </div>
            </div>

        </div>
        

        <div class="right-bloc taille-sup-right"></div>
    </div>    
    <client-only>
        <script>
            // common class
            const container = document.querySelector('.content.index')
            const slider= container.querySelector('.big-diapo .slider')
            let slides = null
            const space = -73
            let state = 0

            let move = (i)=>{
                if(i < 0){
                    i = 0
                    return i
                }else if(i >=4){
                    i =3
                    return i
                }

                slider.style.transform = `translateX(${space*i}vw)`
                return i
            }

            let start = ()=>{
                console.log('plop')
                slides = slider.querySelectorAll('.slide')
                
            }

            window.addEventListener('keydown',(event)=>{
                
                if(event.keyCode === 39){
                    state++
                    console.log(`click right ${state}`)
                    state = move(state)
                }else if(event.keyCode === 37){
                    state --
                    console.log(`click left ${state}`)
                    state = move(state)
                }
            } )

            setTimeout(start(),200)

        </script>
    </client-only>
  </div>
</template>

<script>

import Head from '~/components/Head.vue'
export default {
    created() {

        fetch('http://localhost:3000/data/projects.json')
        .then(r => r.json())
        .then(json => {
            this.projects = json
            let json_temp = [... json]
            this.nb_project = json_temp.length
        })

    },
    head(){
        return{
            title: "Gaetan Avez - Contact Me"
        }
    },
    data(){
        return {
            projects: {},
            nb_project: 0,
        }
    },
  components: {
    Head
  }
}

</script>

<style>
body{
    width:100vw;
    height: 100vh;
    overflow: hidden;
}
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: white
}
/* common */
    .content.index{
        /* padding: 0 15.5%; */
        color: white;
        /* background-color: orange; */
        width: 100vw;
        /* height: calc(1vh*(100 - 15.5)); */
        height: 100vh;
        position: relative;
    }

    .align-row{
        display: flex;
        flex-direction: row;
    }

/* bloc central */
.content.index .central-bloc {
    height: 75%;
    /* background-color: green; */
    position: relative;
}
.content.index .central-bloc .big-diapo{
    height: 75vh;

    position: relative;
}

.content.index .central-bloc .big-diapo .slider{
    will-change: transform;

    transition: transform 0.6s ease-out;
    position: absolute;
    top:0;
    left:0;
    display: flex;
    flex-direction: row;
    z-index: 30;
}

.content.index .central-bloc .big-diapo .slider .slide{
    /* height: 75vh; */
    width: 73vw;

}
.content.index .central-bloc .big-diapo .slider .slide img{
    /* height: 75vh; */
    width: 63vw;
}
.content.index .central-bloc .big-diapo .slider .slide img.responsive_image{
    display: none;
}

.content.index .central-bloc  .project-title{
    position: absolute;
    text-decoration: none;
    color: white;
    top:0%;
    left:0;
    transform: translateY(-100%);

    font-size: 22px;
    font-weight: bold;
    z-index: 9000;
}


.content.index .central-bloc .dots{
    position: absolute;
    left:0;
    bottom: 0;
    transform: translateY( calc(100% + 30px ));

    display: flex;
    flex-direction: row;
}
.content.index .central-bloc .dots .dot{
    width: 10px;
    height: 10px;
    background-color: #191919;
    border-radius: 50%;
    border: none;

    margin-right: 4px;

    cursor: pointer;
    will-change: border;

    transition: border 0.3s ease-out;
}
.content.index .central-bloc .dots .dot.current{
    border: 1.3px solid #979797;
}

.content.index .central-bloc .scroll-to-see{
    position: absolute;
    bottom: 0;
    right: 0;
    transform: translateY( calc(100% + 30px ));

    display: flex;
    flex-direction: row;
    justify-content: space-between;

    text-transform: uppercase;
    font-size: 12px;
    color: white;
    font-family: Arial, Helvetica, sans-serif;


}
.content.index .central-bloc .scroll-to-see img{
    width: 26px;
    height: 26px;

    transform: translateY(-25%);

}


.content.index .central-bloc .state{
    position: absolute;
    bottom: 0;
    right: -2.5%;
    transform: translateY(20%);
    font-family: Arial Black;
    font-style: normal;
    font-weight: 900;
    font-size: 86px;
    /* line-height: 121px; */
    text-align: center;

    /* color: black; */
    color: transparent;
    -webkit-text-stroke: 1px white;
    z-index: -3;

}

/* side bloc common */
.side-diapo{
    position: relative;
    height: 50vh;
    width: 50vw;
    /* background-color: blue; */
    transform: translateY(0);
    clip-path: polygon(1% 0%, 99% 0%, 99% 100%, 1% 100%);
    margin-top:50%;
}
.side-diapo .slider{
    position: absolute;
    top:0;
    left: 0;
    display: flex;
    flex-direction: row;

    will-change: transform;

    transition: transform 0.6s ease-out;
    transform: translateX(0);
}
.side-diapo .slider .slide{
    height: 50vh;
    width: 60vw;
}
.side-diapo .slider .slide img{
    height: 100%;
    width: 100%;
}

/* bloc left */
.content.index .left-bloc{
    height: 100%;
    /* background: red; */
    display: flex;
    justify-content: center;
    align-items: center;
}
.content.index .left-bloc .side-diapo{
    transform: translateX(-60%);
}
.content.index .left-bloc .side-diapo .slider{
    transform: translate(0,0);
}


/* bloc right */
.content.index .right-bloc{
    height: 100%;
    /* background-color: red; */
    display: flex;
    justify-content: center;
    align-items: center;
}
.content.index .right-bloc .side-diapo{
    transform: translateX(60%);
}
.content.index .right-bloc .side-diapo .slider{
    transform: translate(0,0);
}

 @media screen and (max-width: 1024px) {
        .content.index{
            display: none;
        }
    }

</style>
