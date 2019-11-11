<template>
  <div class="container">
    <Head />
    
    <div class="content index align-row">
        <div class="left-bloc taille-sup-left">
            <div class="side-diapo">
                <div class="slider">
                    <div class="slide"></div>
                    <div class="slide">
                        <img src="" alt="">
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
                <div class="slider">
                    
                    <div class="slide">
                        <img src="" alt="">
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
    height: 80%;
    background-color: green;
}

/* side bloc common */
.side-diapo{
    position: relative;
    height: 40vh;
    width: 50vw;
    background-color: blue;
}
.side-diapo .slider{
    position: absolute;
    top:0;
    left: 0;

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
