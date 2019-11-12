<template>
  <div class="container">
    <Head />
    
    <div class="content index align-row">
        <div class="left-bloc taille-sup-left">
            <div class="side-diapo">
                <div class="slider" style="transform:translate(0,0)">

                    <div class="slide"></div>
                    <div class="slide" v-for="item in projects">
                        <img :src="item.project_img" alt="" >
                        <div class="space" style=""></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="taille-5" style="padding-top: 10%; height:100%;">
            <div class="central-bloc taille-5">
                <div style="position: absolute; right:0; bottom:0;">
                    <div style="position:relative">
                        <a  href="" class="project-title"></a>
                        <div class="big-diapo">
                            <div class="slider" style="transform:translate(0,0)">
                                <div class="slide" v-for="item in projects" :data-title="item.project_title" :data-href="item.project_url" >
                                    <img :src="item.project_img" alt="" >
                                    <div class="space" style=""></div>
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
        

        <div class="right-bloc taille-sup-right">
            <div class="side-diapo">
                <div class="slider" >
                    
                    <div class="slide" v-for="item in projects">
                        <img :src="item.project_img" alt="">
                    </div>
                    <div class="slide"></div>
                </div>
            </div>
        </div>
    </div>    
    <client-only>
        <script>
            // common class
                class Slider {
                    constructor(node, xType ,width, nb, start_state =0, y_translation = 0, yType= '%'){
                        this.node = node
                        this.width = width
                        this.nb = nb.length
                        this.xType = xType
                        this.yType = yType
                        this.state = start_state
                        this.y = y_translation

                        if(start_state !== 0 ){
                            
                            this.goTo(start_state)
                        }
                    }

                    next(){
                        //if(this.state < this.nb){
                            this.state ++
                            this.node.style.transform= `translate( -${this.width* this.state}${this.xType},${this.y}${this.yType} )`
                        //}
                    }

                    previous(){
                       // if(this.state > 0){
                            this.state --
                            this.node.style.transform= `translate( -${this.width* this.state}${this.xType},${ this.y}${this.yType} )`
                        //}
                    }

                    goTo(id){
                        this.state = id
                        this.node.style.transform= `translate( -${this.width* id}${this.xType},${ this.y}${this.yType} )`
                    }
                }

                class BigSlider extends Slider{
                    constructor(node, xType ,width, nb ,titleNode, other_button = null,start_state =0, y_translation = 0, yType= '%'){
                        super(node, xType, width, nb)

                        this.slides = nb
                        this.title = titleNode



                        this.titleChange()
                        if(other_button !== null){
                          //  this.otherButtonEvent()
                        }
                        //console.log(this.nb)
                        //console.log(this)

                    }
                    next(){
                        super.next()
                        this.titleChange()
                    }
                    previous(){
                        super.previous()
                        this.titleChange()
                    }
                    goTo(id){
                        super.goTo(id)
                        this.titleChange()
                    }


                    otherButtonEvent(){
                        this.other_button.addEventListener('click', (event)=>{
                            event.preventDefault()
                            this.next()
                        })
                    }
                    
                    scrollEvent(nodeToScroll){
                        this.nodeToScroll = nodeToScroll

                        //ToDo
                    }

                    dotChangeState(){
                        
                    }

                    counterChangeState(){

                    }

                    titleChange(){
                        const urlPrefix = "/projects/"
                        this.title.innerHTML = this.slides[this.state].dataset.title
                        this.title.href = `${urlPrefix}${this.slides[this.state].dataset.href}`
                        console.log( this.slides[this.state].dataset.title)
                        
                    }
                }



                //CODE

                // slider
                let content = document.querySelector('.content.index')

                let left_slider 
                let right_slider 
                let big_slider 
                let title 

                let left_slide 

                let right_slide 

                let big_slide 
                let dot
                let state_node

                let run = ()=>{
                    left_slider = content.querySelector('.left-bloc .side-diapo .slider')
                    right_slider = content.querySelector('.right-bloc .side-diapo .slider')
                    big_slider = content.querySelector('.central-bloc .big-diapo .slider')
                    title = content.querySelector('.central-bloc a.project-title')
                    dots = content.querySelectorAll('.central-bloc .dots .dot')
                    state_node = content.querySelector('.central-bloc .state')

                    left_slide = new Slider(left_slider,'vw',60,left_slider.querySelectorAll('.slide')  )

                    right_slide = new Slider(right_slider,'vw',60,right_slider.querySelectorAll('.slide'),1 )

                    big_slide = new BigSlider(big_slider, 'vw', 63, [...big_slider.querySelectorAll('.slide')],title )

                    dotEvent(dots)
                }

                let global_state = 0

                //slider function
                let nextSlide = ()=>{
                    global_state ++

                    left_slide.next()
                    big_slide.next()
                    right_slide.next()

                    dotState(global_state)
                }

                let previousSlide = ()=>{
                    global_state --
                    left_slide.previous()
                    big_slide.previous()
                    right_slide.previous()
                    console.log(global_state)
                    dotState(global_state)
                }

                let goToSlide = (id)=>{
                    
                    id = parseInt(id)
                    left_slide.goTo(id)
                    big_slide.goTo(id)
                    right_slide.goTo(id+1)
                    dotState(id)
                }

                let dotEvent = (dots)=>{
                    dots[0].classList.add('current')
                    for(let i=0; i<dots.length; i++){
                        dots[i].dataset.slideNb = i
                        dots[i].addEventListener('click', (event)=>{
                            event.preventDefault()

                            const state = dots[i].dataset.slideNb
                            goToSlide(state)

                            
                        })
                    }
                }

                let dotState = (id)=>{
                    for(let j =0; j<dots.length; j++){
                        dots[j].classList.remove('current')
                    }
                    dots[id].classList.add('current')
                    stateNb(id)
                }


                let stateNb = (id)=>{
                    state_node.innerHTML = `0${id+1}`
                    console.log(state_node)
                }

                setTimeout(()=>{
                    run()
                    console.info("runnig")
                },500)
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
    width: 63vw;
    clip-path: polygon(0% 0, 100% 0%, 100% 100%, 0 100%);
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
    height: 75vh;
    width: 63vw;

}
.content.index .central-bloc .big-diapo .slider .slide img{
    height: 100%;
    width: 100%;
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
    right: -9.5%;
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
</style>
