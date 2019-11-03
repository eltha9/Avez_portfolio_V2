<template>
  <div class="container">
    <Head />
    
    <div class="window-text">
        <span class="first">Welcome to my</span>
        <span class="second">portfolio</span>
    </div>
    <main>
        <div class="last">
            <div class="content">
                <img src="~/assets/images/projects/Unsplash.png" alt="">
                <img src="~/assets/images/projects/Blog.png" alt="">

            </div>
        </div>


        <div class="content">
            <a href="#">
                <div class="id">01</div>
                <div class="contour"></div>
                <div class="project">
                    <h2>CONCEPT PAGE UNSPLASH</h2>
                    <div class="img">
                        <div class="sub-img">
                            <div class="content">
                                <img src="~/assets/images/projects/Unsplash.png" alt="">
                                <img src="~/assets/images/projects/Blog.png" alt="">
                                <img src="~/assets/images/projects/richard.png" alt="">
                            </div>
                        </div>
                    </div>
                </div>

            </a>
        </div>


        <div class="next">
            <div class="content">

                <img src="~/assets/images/projects/Blog.png" alt="">
                <img src="~/assets/images/projects/richard.png" alt="">
            </div>
        </div>
    </main>

    <div class="next-button">
        <img src="~/assets/images/project_button.svg" alt="">
    </div>
    <div class="last-button">
        <img src="~/assets/images/project_button.svg" alt="">
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
