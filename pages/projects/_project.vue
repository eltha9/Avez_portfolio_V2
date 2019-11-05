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
            <div class="row align row taille-5">
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
                <!-- <img src="" alt="">{{next.img}} -->
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
    .content.project .page_title{
        
    }
    .content.project .post_type{

    }
    .content.project .post_name{

    }
    .content.project .project_date{

    }
    .content.project .project_type{

    }
    .content.project .project_top_description{

    }
    .content.project .project_slogan{

    }
    .content.project .project_main_text{

    }
    /* next project */
    .content.project .next-project{

    }
</style>