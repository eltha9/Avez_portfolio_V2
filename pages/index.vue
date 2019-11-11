<template>
  <div class="container">
    <Head />
    
    <div class="content index align-row">
        <div class="left-bloc taille-sup-left">
            <div class="side-diapo">
                <div class="slider">

                    <div class="slide"></div>
                    <div class="slide" v-for="item in projects">
                        <img :src="item.project_img" alt="">
                    </div>
                </div>
            </div>
        </div>

        <div class="taille-5" style="padding-top: 10%; height:100%;">
            <div class="central-bloc taille-5">
                
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

// common class
class Slider {
    constructor(node,width, nb, start_state =0, y_translation = 0){
        this.node = node
        this.width = width
        this.nb = nb

        this.state = start_state
        this.y = y_translation

        if(start_state !== 0 ){
            this.goTo(start_state)
        }
    }

    next(){
        this.state ++
        this.node.style.transform= `translate( ${this.width* this.state},${ this.y} )`
    }

    previous(){
        this.state --
        this.node.style.transform= `translate( ${this.width* this.state},${ this.y} )`
    }

    goTo(id){
        this.node.style.transform= `translate( ${this.width* id},${ this.y} )`
    }
}

class BigSlider extends Slider{
    constructor(dot_node, other_button = null){
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
    
    scrollEvent(){
        //ToDo
    }
}

// code
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
}

/* side bloc common */
.side-diapo{
    position: relative;
    height: 40vh;
    width: 50vw;
    background-color: blue;
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
    background: red;
    display: flex;
    justify-content: center;
    align-items: center;
}
.content.index .left-bloc .side-diapo{
    transform: translateX(-60%);
}


/* bloc right */
.content.index .right-bloc{
    height: 100%;
    background-color: red;
    display: flex;
    justify-content: center;
    align-items: center;
}
.content.index .right-bloc .side-diapo{
    transform: translateX(60%);
}
</style>
