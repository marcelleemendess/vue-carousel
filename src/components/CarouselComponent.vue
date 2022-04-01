<template>
  <div class="carousel">
      <slot :currentSlide="currentSlide"/>
  </div>
</template>

<script>
import { ref } from 'vue'; 
export default {
  setup(){
    const currentSlide = ref(1) // using the index array 

    return { currentSlide };
  }
}
</script>

<style>

</style>