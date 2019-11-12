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
                    </div>
                </div>
            </div>
        </div>

        <div class="taille-5" style="padding-top: 10%; height:100%;">
            <div class="central-bloc taille-5">
                <div style="position: absolute;width:60vw; right:0; bottom:0;">
                    <div class="big-diapo">
                        <h2 class="project-title"></h2>
                        <div class="slider" style="transform:translate(0,0)">
                            <div class="slide" v-for="item in projects" :data-title="item.project_title" >
                                <img :src="item.project_img" alt="" >
                            </div>
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
                        this.nb = nb
                        this.xType = xType
                        this.yType = yType

                        this.state = start_state
                        this.y = y_translation

                        if(start_state !== 0 ){
                            this.goTo(start_state)
                        }
                    }

                    next(){
                        this.state ++
                        this.node.style.transform= `translate( -${this.width* this.state}${this.xType},${this.y}${this.yType} )`
                    }

                    previous(){
                        this.state --
                        this.node.style.transform= `translate( -${this.width* this.state}${this.xType},${ this.y}${this.yType} )`
                    }

                    goTo(id){
                        this.node.style.transform= `translate( ${this.width* id}${this.xType},${ this.y}${this.yType} )`
                    }
                }

                class BigSlider extends Slider{
                    constructor(dot_node, other_button = null){
                        //super()
                        this.dot_node = dot_node
                        this.dots = this.dot_node.querySelectorAll('dot')

                        this.dotEvent()

                        if(other_button !== null){
                            this.otherButtonEvent()
                        }

                    }

                    dotEvent(){
                        for(let i=0; i<this.dots.length; i++){
                            this.dots.dataset.slideNb = i
                            this.dots[i].addEventListener('click', (event)=>{
                                event.preventDefault()
                                this.goTo(this.dots[i].dataset.slideNb)
                            })
                        }
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
                        
                    }
                }

                //CODE

                // SLIDER
                let content = document.querySelector('.content.index')

                const left_slider = content.querySelector('.left-bloc .side-diapo .slider')
                const right_slider = content.querySelector('.right-bloc .side-diapo .slider')
                const big_slider = content.querySelector('.central-bloc .big-diapo .slider')

                let left_slide = new Slider(left_slider,'vw',50,left_slider.querySelectorAll('.slide').length )

                let right_slide = new Slider(right_slider,'vw',50,right_slider.querySelectorAll('.slide').length )

                //let big_slide = new BigSlider()

                

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
    background-color: green;
    position: relative;
}
.content.index .central-bloc .big-diapo{
    height: 60vh;
    width: 60vw;
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
}

.content.index .central-bloc .big-diapo .slider .slide{
    height: 60vh;
    width: 60vw;

}
.content.index .central-bloc .big-diapo .slider .slide img{
    height: 100%;
    width: 100%;
}



/* side bloc common */
.side-diapo{
    position: relative;
    height: 40vh;
    width: 50vw;
    /* background-color: blue; */
    transform: translateY(0);
    clip-path: polygon(0% 0, 100% 0%, 100% 100%, 0 100%);
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
    height: 40vh;
    width: 50vw;
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
