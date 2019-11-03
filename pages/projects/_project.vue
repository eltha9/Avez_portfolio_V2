<template>
    <div class="container">
        <Head />
        <div class="content project" style="color:white">
            {{json}}
        </div>
    </div>
</template>

<script>
import Head from '~/components/Head.vue'

export default {
    created() {
        let title = this.$route.params.project

        fetch(`/data/${title}.json`)
        .then(r => r.json())
        .then(json => {
            this.json = json
        })
    },
    data(){
        
        return {
            data : this.json
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
        padding-top: 10%;
    }
    .content.project{

    }
</style>