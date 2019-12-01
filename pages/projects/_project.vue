<template>
    <div class="container">
        <Head />
        <div class="main-image-to-body">
            <div style="position:relative;width:100%;">

                <img :src="json.main_image" :alt="json.page_title + 'Home page'" class="not-responsive-main-image">
                <img :src="json.main_image_responsive" :alt="json.page_title + 'Home page'" class="responsive-main-image">
                <div class="call-to-scroll">
                    <span class="text">scroll</span>
                    <span class="vertical-bar"></span>
                </div>
            </div>
            
        </div>
        <div class="content project">
            <div class="main_image taille-5"></div>
            <h1 class="page-title">{{json.page_title}}</h1>
            <div class="row taille-1 align-row ux">
                <span class="post-type">{{json.post_type}}</span>
                <div class="line"></div>
                <span class="post-name">{{json.post_name}}</span>
            </div>
            <div class="row taille-5 chapeau">
                <div class="top-description">
                    <div class="taille-1 project-date">
                        {{json.project_date}}
                    </div>
                    <div class="taille-1 project-type">
                        {{json.project_type}}
                    </div>
                </div>
                <div class="taille-3 project-top-description">
                    {{json.project_top_description}}
                </div>
            </div>
            <div class="row align-row">
                <div class="taille-5 project-slogan-container">
                    <h2 class="project-slogan">{{json.project_slogan}}</h2>
                </div>
            </div>
            <div class="row align-row">
                <div class="taille-2 mockup-div">
                    <img class="mockup" src="~/assets/images/mockup_png.png" alt="">
                    <div class="inside-mockup">
                        <img  :src="json.project_mockup_img" alt="">
                    </div>

                </div>
                <div v-html="json.project_main_text" class="taille-3 project-main-text">
                </div>
            </div>
            <div class="bottom-images row">
                <div class="border">
                    <div class="inside">
                        <img :src="json.project_bottom_img" alt="">
                    </div>
                </div>
            </div>

            <div class="next-project taille-5 row">
                <h3>Next project:</h3>
                <a :href="json.next_project_link" >{{json.next_project_name}}</a>
                <div class="taille_5 image-next">
                    <img :src="json.next_project_img" alt="">
                </div>
            </div>
            <client-only>
                <script>
                    //comon 

                    const project_container = document.querySelector('.content.project')

                    //slogan slider 
                    let project_slogan =  {
                        node : project_container.querySelector('.project-slogan')
                        
                        }
                    let slogan_direction = 0
                    let window_height = window.innerHeight
                    project_slogan.bouding = project_slogan.node.getBoundingClientRect()

                    window.addEventListener('rezise', ()=>{
                        window_height = window.innerHeight
                        project_slogan.bouding = project_slogan.node.getBoundingClientRect()
                    })

                    window.addEventListener('scroll', (event)=>{
                            slogan(event)
                            paralax_effect()

                    })

                    let slogan = (event) =>{
                        project_slogan.bouding = project_slogan.node.getBoundingClientRect()

                        if( project_slogan.bouding.top < window_height){
                            slogan_direction =  project_slogan.bouding.top - window_height 

                            /*if(slogan_direction > 0){
                                slogan_direction = 0
                            }
                                voir avec gaetan pour le scroll si il faut l'arreter ou non
                            */

                            project_slogan.node.style.right = `${slogan_direction}px`
                        }
                    }

                    let paralax = (event)=>{

                    }

                    //mockup scroll

                    const mockup_div = project_container.querySelector('.mockup-div')

                    let mockup = {
                        event_node: mockup_div.querySelector('img.mockup'),
                        scrolling_node: mockup_div.querySelector('.inside-mockup img'),
                        translate: 0,

                    }
                    mockup.bounding = mockup.scrolling_node.getBoundingClientRect()

                    const space = 19

                    
                    
                    mockup.event_node.addEventListener('wheel',(event)=>{
                        event.preventDefault()
                        const height = mockup.scrolling_node.getBoundingClientRect().height
                        const mockup_height = mockup.event_node.getBoundingClientRect().height
                        let limit = (height - mockup_height) * -1 
                        //console.log(height)
                        
                        if(event.deltaY < 0){
                            if((mockup.translate + space) <= 0){
                                mockup.translate += space 

                            }

                        }else if(event.deltaY > 0 ){

                                //console.log(`translate : ${mockup.translate}, calc: ${-(height - mockup_height +100)} `)

                            //if( (mockup.translate - space) => limit ){
                                mockup.translate -= space 
                            //}
                        }

                        //console.log(mockup.translate)
                        mockup.scrolling_node.style.transform = `translateY(${mockup.translate}px)`
                    })


                    // paralax
                    let paralax_image = project_container.querySelector('.bottom-images .border .inside img')
                    let paralax_container = project_container.querySelector('.bottom-images .border .inside')
                    let paralax_sinus = 50

                    let paralax_effect = ()=>{
                        let bounding =  paralax_container.getBoundingClientRect()
                        //console.log(bounding)
                        if( ( bounding.top+(bounding.height/4) ) < window_height){
                            paralax_sinus = bounding.top - window_height
                            //console.log(50+paralax_sinus/10)
                            paralax_image.style.top = `${50+paralax_sinus/50}%`

                        }
                    }

                </script>
            </client-only>
        </div>
    </div>
</template>

<script>
import Head from '~/components/Head.vue'

export default {
    created() {
        let title = this.$route.params.project

        fetch(`http://localhost:3000/data/${title}.json`)
        .then(r => r.json())
        .then(json => {
            this.json = json
            this.next = json.next_project
            console.log(this.json)
        })

    },
    head(){
        return{
            title: `Gaetan Avez - ${this.json.page_title} project`
        }
    },
    data(){
        return {
            values : this.json,
            test : "this.json",
            json: {},
            next:{}
        }
    },
    components:{
        Head
    }
}
</script>

<style>
    body{
        width: 100vw;
        height: 100%;
        /* height: content; */

        /* padding-top: 10%; */
        overflow-x: hidden;
    }
    /* common */
    .content.project{
        padding: 10% 15.5% 0 15.5%;
        color: white;
        /* background-color: orange; */

    }

    .align-row{
        display: flex;
        flex-direction: row;
    }

    .main-image-to-body{
        position: absolute;
        top:0;
        left: 0;
        z-index: 0;
        /* height: 104vh; */
        height: 103vh;
        width: 100vw;
    }
    .main-image-to-body img.not-responsive-main-image{
        height: 100%;
        width: 100%;
    }
    .main-image-to-body img.responsive-main-image{
        height: 100%;
        width: 100%;
        display: none;
    }

    .main-image-to-body .call-to-scroll{
        position: absolute;
        display: flex;
        flex-direction: column;
        /* justify-content: center; */
        align-items: center;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
    }
    .main-image-to-body .call-to-scroll .text{
        text-transform: uppercase;
        color: black;
        font-size: 18px;
        font-weight: bold;
        margin-bottom: 16px;
        mix-blend-mode: difference;
    }
    .main-image-to-body .call-to-scroll .vertical-bar{
        width:4px;
        height: 40px;
        background-color: black;
        mix-blend-mode: difference;
    }


    /* main image */
    .content.project .main_image{
        /* width: 100vw; */
        /* height: calc(100vh - 15.5vh); */
        height: calc(100vh - 15.5vh);
        /* background-color: green; */
        position: relative;
    }
    .content.project .main_image img{ /*reduction de la taille de la photo*/
        width: 100vw;
        /* height: 100vh;  */
        z-index:-3;
        position: absolute;
        /* top:-16.5vh; -15.5*/
        top: -25.5%;
        left:-15.5vw;
    }

    /* main content */
    .content.project h1.page-title{
        color: white;
        font-size: 64px;
        margin-top: 120px;
        margin-bottom: 7px;
    }
    .content.project .post-type{
        color:white;
        font-size: 18px;
    }
    .content.project .post-name{
        color:white;
        font-size: 18px;
    }
    .content.project .project-date{
        color: #A6A6A6;
        font-size: 22px;
    }
    .content.project .project-type{
        color: #A6A6A6;
        font-size: 22px;
    }
    .content.project .project-top-description{
        color: #A6A6A6;
        font-size: 22px;
    }

    .content.project .project-slogan-container{
        position: relative;
        height: 64px;
        margin-bottom: 100px;
    }
    .content.project .project-slogan-container .project-slogan{
        position: absolute;
        top:0;
        right: 0;
        color: white;
        font-size: 64px;
        white-space: nowrap;
        will-change: right;

        margin:0;
    }


    .content.project .project-main-text{
        color: #A6A6A6;
        font-size: 22px;
        display: flex;
        align-items: center;
    }

    .content.project .line{
        width: 45px;
        height: 1px;
        background-color: white;
        margin: auto 10px;
    }

    .content.project .mockup-div{
        position: relative;
    }
    .content.project .mockup-div .mockup{
        width: 75%;
    }

    .content.project .mockup-div .inside-mockup{
        position: absolute;
        width: 68%;
        height: 92%;
        overflow: scroll;
        top:0;
        z-index: -1;
        transform: translate(5%, 4%);
    }
    .content.project .mockup-div .inside-mockup img{
        width: 100%;
        will-change: transform;
    }

    /* .content.project .mockup-div{
        position: relative;
    }
    .content.project .mockup-div .mockup{
        position: absolute;
        top:0;
        left: 0;
        z-index: 70;
        width: calc(13.8vw *1.5);
        
    }
    .content.project .mockup-div .inside-mockup{
        position: absolute;
        z-index: 60;
        top:50%;
        left: 50%;

        transform: translate(-50%,-50%);

        width: calc(13.8vw *1.5);
        height: 100%;
        overflow-y:scroll;
    }
    .content.project .mockup-div .inside-mockup{
        width: calc(13.8vw *1.5);
        height: 100%;
    } */
    /* bottom image || paralax */
    .content.project .bottom-images{
        height: 95vh;

        margin-top: 100px;
        margin-bottom: 140px;

        position: relative;
    }
    .content.project .bottom-images .border{
        position: absolute;
        width: 100vw;
        height: 100%;
        top:0;
        left: -15.5vw;
        background-color: black;
        overflow: hidden;
    }
    .content.project .bottom-images .border .inside{
        width: 100%;
        height: 100%;
        position: relative;
    }
    .content.project .bottom-images .border .inside img{
        width: 140%;
        position: absolute;
        left:50%;
        top:50%;
        transform: translate(-50%,-50%);
        will-change: top;
        /* transform-origin: 0% 0%; */
        /* transform: rotateZ(45deg); */
    }


    /* next project */
    .content.project .next-project{
        text-align: center;
    }
    .content.project .next-project h3{
        font-size: 32px;
        color: white;
        margin-bottom: 18px;
    }
    .content.project .next-project a{ 
        font-size: 24px;
        color: #A6A6A6;
        
    }
    .content.project .next-project .image-next{
        height: 14.5vw;
        overflow: hidden;
        margin-top: 80px;
    }
    .content.project .next-project .image-next img{
        width: 100%;
    }

    /* bloc margin  */
    .content.project .ux{
        margin-bottom: 74px;
    }   

    .content.project .chapeau{
        margin-bottom: 46px;
        display: flex;
        flex-direction: row;
    } 
    .content.project .chapeau .top-description{
        display: flex;
        flex-direction: row;
        width: 100% !important; 
    }

    @media screen and (max-width: 1024px) {
        body{
            width: 100vw;
            overflow-x: hidden;
        }
        .container{
            overflow-x: hidden;
        }

        .content.project{
            padding: 10% 6.4% 0 6.4%;
        }

        .main-image-to-body{
            height: auto;
        
        }
        
        .main-image-to-body img.not-responsive-main-image{
            height: 100%;
            width: 100%;
            display: none;
        }
        .main-image-to-body img.responsive-main-image{
            height: auto;
            width: 100%;
            display: inherit;
        }

        .content.project .main_image{
            height: calc(50vh)
        }

        .content.project h1.page-title{
            color: white;
            font-size: 32px;
            margin-top: 140px;
            margin-bottom: 12px;
        }
        .content.project .post-type{
            color:white;
            font-size: 16px;
        }
        .content.project .post-name{
            color:white;
            font-size: 16px;
        }
        .content.project .project-date{
            color: #A6A6A6;
            font-size: 16px;
        }
        .content.project .project-type{
            color: #A6A6A6;
            font-size: 16px;
        }
        .content.project .project-top-description{
            color: #A6A6A6;
            font-size: 16px;
        }

        .content.project .ux{
            margin-bottom: 30px;
        }

        .content.project .chapeau{
            margin-bottom: 32px;
            display: flex;
            flex-direction: column;
        } 
        .content.project  .chapeau .top-description{
            margin-bottom: 24px;
        }
        .content.project .project-slogan-container{
            margin-bottom: 30px;
            height: 40px;
        }
        .content.project .project-slogan-container .project-slogan{
            font-size: 32px; 
        }


        /* paralax responsive  */
        .content.project .bottom-images .border{
            /* height: 10vh; */
        }
        .content.project .bottom-images .border{
            width: 100vw;
            left: -6.4vw;
        }
    }
</style>