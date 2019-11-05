<template>
    <div class="container">
        <Head />
        <div class="content project">
            <div class="main_image">

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
            console.log(this.json)
        })

    },
    data(){
        return {
            values : this.json,
            test : "this.json",
            json: {}
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
        height: 100vh;
        overflow: hidden;
        /* padding-top: 10%; */
    }
    .content.project{
        color: white;
        background-color: orange;
        height: 30vh;
    }

    .content.project .main_image{
        
    }
</style>