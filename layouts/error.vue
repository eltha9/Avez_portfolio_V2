<template>
    <div class="container">
        <Head/>
        <div class="content">
            <img src="~/assets/images/404.png" alt="">
            <div>
                <span class="title">404</span>
                <span class="sub-title">Oups… you’r lost</span>
            </div>
        </div>
    </div>
</template>

<script>
import Head from '~/components/Head.vue'
export default {
    components: {
        Head
    }
}
</script>

<style>
    .content{
        position:relative
    }
    .content img{
        position:absolute;
        left: 50%;
        top:50%;
        transform: translate(-50%,-50%);
        z-index: 90;
    }
    .content div{
        position: absolute;
        left:50%;
        top: 50%;
        transform: translate(-50%, -50%);
        z-index: 100;
        text-align: center
    }
    .content div span.title{
        font-size: 308px;
        letter-spacing: 15px;
        color: white;
    }
    .content div span.sub-title{
        font-size: 18px;
        letter-spacing: 0.68px;
        color: white;
    }
</style>