<template>
    
    <div class="container">
        <Head />
        <div class="content contact ">
            <div class="top">
                <h1>Leave me a message</h1>
                <span>Or by email: gaetan.avez@gmail.com </span>
            </div>
            <form action="#" class="taille-5">

                <div class="row align-row">
                    <div class="taille-2">
                        <label>
                            Name :
                            <input type="text">
                        </label>
                    </div>
                    <div class="taille-3">
                        <label>
                            Email :
                            <input type="email">
                        </label>
                    </div>

                </div>
                <div class="row taille-4">
                    <textarea name="" id="" cols="30" rows="10">Hello Gaetan, </textarea>
                </div>
                <div class="row taille-1 bottom">
                    <div class="taille-1 contact-row">
                        <input type="submit" value="Send it">
                        <img src="~/assets/images/send_button.svg" alt="">
                    </div>
                </div>


            </form>

        </div>
    </div>
</template>

<script>
import Head from '~/components/Head.vue'
export default {
    head(){
        return{
            title: "Gaetan Avez - Contact Me"
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

    .content.contact{
        padding: 0 15.5%;
        padding-top: 10%;
        height:  calc(1vh*(100 - 15.5));

        color: white;
        display: flex;
        flex-direction: column;
    }
    /* common */
    .content.contact .align-row{
        display: flex;
        flex-direction: row;
    }

    /* top */
    .content.contact .top{
        margin-bottom: 68px;
    }
    .content.contact .top h1{
        font-size: 62px;
        letter-spacing: -1.1px;
        margin: 0;
    }
    .content.contact .top span{
        color: #A6A6A6;
        font-size: 18px;
    }

    /* form  */
    .content.contact label{
        font-size: 24px;
    }
    .content.contact label input{
        width: 70%;
        background-color: transparent;
        border: none;
        font-size: 24px;
        color:white;
        
        
    }
    .content.contact textarea{ /* afficher une ligne blanche en dessous quand on clic dessus*/ 
        margin-top: 45px;
        font-size: 24px;
        width: 100%;
        text-align: left;
        color:white;
        background-color: transparent;
        border:none;
        resize: none;

    }
    .content.contact form{
        flex-grow: 100;
        position: relative;
    }
    /* bottom */
    .content.contact form .bottom{
        position: absolute;
        right: 0;
        bottom: 5%;
        cursor: pointer;

    }
    .content.contact .contact-row{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }
    .content.contact .bottom input[type = submit]{
        font-size: 24px;
        color:#A6A6A6;
        border: none;
        background-color: transparent;
        text-decoration: none;
        padding: 0;
        cursor: pointer;
    }
    .content.contact .bottom img{
        vertical-align: middle;
        width: 32px;
        height: 32px;
    }

</style>