<template>
  <div class="container">
    <Head />
    
    <div class="content index">

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

        })

    },
    data(){
        return {
            projects: {},
        }
    },
  components: {
    Head
  }
}
</script>

<style>
body{
    overflow: hidden;
}
/* common */
    .content.index{
        padding: 0 15.5%;
        color: white;

    }

    .align-row{
        display: flex;
        flex-direction: row;
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
</style>
