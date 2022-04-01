<template>
  <div class="carousel">
      <slot :currentSlide="currentSlide"/>

      <!-- Navigation -->
      <div class="navigate">
        <div class="toggle-page left">
          <i @click="prevSlide" class="fas fa-chevron-left"></i>
        </div>
        <div class="toggle-page right">
          <i @click="nextSlide" class="fas fa-chevron-right"></i>
        </div>
      </div>

      <!-- Pagination -->
      <div class="pagination">
        <span 
          @click="goToSlide(index)"
          v-for="(slides, index) in getSlideCount"
          :key="index"
          :class="{active: index + 1 === currentSlide }" 
        >
        </span>
      </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'; 
export default {
  setup(){
    const currentSlide = ref(1); // start with 1, to follow the slides by quantity, not index
    const getSlideCount = ref(null); //before page mount, we have access to the amount of slides
    const autoPlayEnabled = ref(true);
    const timeoutDuration = ref(5000);

    //Next slide
    const nextSlide = () => {
      currentSlide.value === getSlideCount.value ? currentSlide.value = 1 : currentSlide.value += 1;
    }

    //Prev slide
    const prevSlide = () => {
      currentSlide.value === 1 ? currentSlide.value = getSlideCount.value : currentSlide.value -= 1;
    }

    const goToSlide = (index) => {
      currentSlide.value = index + 1
    }

    const autoPlay = () => {
       setInterval(() => {
         nextSlide()
       }, timeoutDuration.value);
    }
      if (autoPlayEnabled.value) {
        autoPlay();
      }

    onMounted(() => {
      //when the pag mounted, we set getSlideCount = to the amount of slides present, like this the  functions to increment and decrement the number of slides it will always work.
      getSlideCount.value = document.querySelectorAll(".slide").length;
    });

    return { currentSlide, nextSlide, prevSlide, getSlideCount, goToSlide};
  },
};
</script>

<style lang="scss">
  .navigate {
    display: flex;
    justify-content: center;
    align-items: center;

    padding: 0 16px;
    height: 100%;
    width: 100%;
    position: absolute;

    .toggle-page {
      display: flex;
      flex: 1;  // to get a igual amount of space
    }

    .right {
      justify-content: flex-end;
    }

    i {
      cursor: pointer;
      display: flex;
      justify-content:center;
      align-items: center;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      background-color: #6347c7;
      color: white;
    }
  }
  
  .pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 16px;
    
    position: absolute;
    bottom: 24px;
    width: 100%;

    span {
      cursor: pointer;width: 20px;
      height: 20px;
      border-radius:50%;
      background-color: white;
    }

    .active {
      background-color: #6347c7;
    }
    
  }
</style>