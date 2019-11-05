<template>
    <div class="container">
        <Head />
        <div class="content project">
            <div class="main_image">
                <img src="" :alt="json.page_title + 'Home page'">
            </div>
            <h1>{{json.page_title}}</h1>
            <div class="row taille-1">
                <span class="post-type">{{json.post_type}}</span>
                <div class="line"></div>
                <span class="post-name">{{json.post_name}}</span>
            </div>
            <div class="row align-row taille-5">
                <div class="taille-1 project-date">
                    {{json.project_date}}
                </div>
                <div class="taille-1 project-type">
                    {{json.project_type}}
                </div>
                <div class="taille-3 project-top-description">
                    {{json.project_top_description}}
                </div>
            </div>
            <div class="row align-row">
                <div class="taille-1" >

                </div>
                <div class="taille-4">
                    <h2 class="project-slogan">{{json.project_slogan}}</h2>
                </div>
            </div>
            <div class="row align-row">
                <div class="taille-2">
                    <img class="mockup" src="" alt="">
                    <img class="inside-mockup" src="" alt="">
                </div>
                <div v-html="json.project_main_text" class="taille-3 project-main-text">
                </div>
            </div>
            <div class="bottom-images row">
                
            </div>

            <div class="next-project taille-5 row">
                <h3>Next project:</h3>
                <!-- <a href="{{next.link}}">{{next.name}}</a> -->
                <div class="taille_5 image-next">
                <!-- <img src="" alt="">{{next.img}} -->
                </div>
            </div>
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

        padding-top: 10%;
    }
    /* common */
    .content.project{
        padding: 0 15.5%;
        color: white;
        /* background-color: orange; */
        height: 30vh;
    }

    .align-row{
        display: flex;
        flex-direction: row;
    }
    /* main image */
    .content.project .main_image{
        width: 100vw;
        height: 100vh;
        /* background-color: green; */
    }
    .content.project .main_image img{
        width: 100%;
        height: 100%; 
    }

    /* main content */
    .content.project .page-title{
        color: white;
        font-size: 64px;
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
    .content.project .project-slogan{
        color: white;
        font-size: 64px;
    }
    .content.project .project-main-text{
        color: #A6A6A6;
        font-size: 22px;
    }
    /* next project */
    .content.project .next-project{

    }
    .content.project .next-project h3{
        font-size: 32px;
        color: white;
    }
    .content.project .next-project a{ 
        font-size: 24px;
        color: #A6A6A6;
    }
    .content.project .next-project .image-next{
        height: 20%;
    }
    .content.project .next-project .image-next img{
        width: 100%;
    }
</style>