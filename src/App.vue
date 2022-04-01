<template>
  <div class="home">
    <CarouselComponent class="carousel" v-slot="{ currentSlide }">
      <SlideComponent v-for="(slide, index) in carouselSlides" :key="index">
        <!-- the components are nested because the tag slot it will 
        be replaced for whatever we put inside the componentes -->
        <div v-show="currentSlide === index + 1" class="slide-info">
          <img :src="require(`./assets/${slide}.jpeg`)" alt="" />
        </div>
      </SlideComponent>
    </CarouselComponent>
  </div>

</template>

<script>
import CarouselComponent from "./components/CarouselComponent";
import SlideComponent from "./components/SlideComponent";

export default {
  name: 'App',
  components: {
   CarouselComponent,
   SlideComponent
  },
  setup(){
    const carouselSlides = ['image-1', 'image-2', 'image-3']
      return {
        carouselSlides
      }
  }
}
</script>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .carousel {
    position: relative;
    max-height: 100vh;
    height: 100vh;

    .slide-info {  
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      max-height: 100%;
      height: 100%;

      img {
        min-width: 100%;
        height: 100%;
        object-fit: cover;
      }
      
    }
  }

</style>
