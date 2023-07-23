<script setup>
import { ref, reactive } from 'vue'

/* Slider Current Index */
const cureentIndx = ref(0)

/* Slider items */
const slides = [
  {
    title: 'First slide label',
    shortDisc: 'Some representative placeholder content for the first slide.',
    imgSrc: "https://tecdn.b-cdn.net/img/Photos/Slides/img%20(15).jpg",
    alt: 'slide one image'
  },
  {
    title: 'Second slide label',
    shortDisc: 'Some representative placeholder content for the second slide.',
    imgSrc: "https://tecdn.b-cdn.net/img/Photos/Slides/img%20(22).jpg",
    alt: 'slide two image'
  },
  {
    title: 'Third slide label',
    shortDisc: 'Some representative placeholder content for the third slide.',
    imgSrc: "https://tecdn.b-cdn.net/img/Photos/Slides/img%20(23).jpg",
    alt: 'slide three image'
  }
]

/* next and previous  */
const gotoNextItem = () => {
  cureentIndx.value++
  if( cureentIndx.value > slides.length-1 ){
    cureentIndx.value = 0
  }
}

const gotoPevioustItem = () => {
  cureentIndx.value--
  if( 0 > cureentIndx.value  ){
    cureentIndx.value = slides.length-1
  }
}

/* Auto paly */
const autPlayInstance = ref('')
const startAutoPlay = () =>{ autPlayInstance.value = setInterval(gotoNextItem, 3000) }
const stopAutoPlay = () =>{ clearInterval(autPlayInstance.value) }
startAutoPlay();

</script>

<template>
  <h1 class="text-center my-7 text-xl">Image Carousel</h1>
  <div @mouseover="stopAutoPlay()"  @mouseleave="startAutoPlay()" id="carouselExampleCaptions" class="relative">
  <!--Carousel indicators-->
    <div class="absolute bottom-0 left-0 right-0 z-[2] mx-[15%] mb-4 flex list-none justify-center p-0">
      <button 
        v-for="(item, index) in slides.length"
        :key = "item"
        @click="cureentIndx = index"
        type="button"
        :class="cureentIndx == index ? '!opacity-100' : ''"
        class="mx-[3px] box-content h-[3px] w-[30px] flex-initial cursor-pointer border-0 border-y-[10px] border-solid border-transparent bg-white bg-clip-padding p-0 -indent-[999px] opacity-50 transition-opacity duration-[600ms] ease-[cubic-bezier(0.25,0.1,0.25,1.0)] motion-reduce:transition-none focus:outline-0 hover:border-transparent"></button>
    </div>

    <!--Carousel items-->
    <div class="relative w-full overflow-hidden after:clear-both after:block after:content-['']">
      <!--First item-->
      <div 
        v-for="(slide, index) in slides"
        :key = "index"
        :class=" cureentIndx == index ? '!opacity-100' : '' "
        class="relative float-left -mr-[100%] w-full opacity-0 transition-opacity duration-[800ms] ease-[cubic-bezier(0.25,0.1,0.25,1.0)] motion-reduce:transition-none">
        <img class="w-full" :src="slide.imgSrc" :alt="slide.alt" />
        <div class="absolute inset-x-[15%] bottom-5 py-5 text-center text-white md:block">
          <h5 class="text-xl">{{ slide.title }}</h5>
          <p>{{ slide.shortDisc }}</p>
        </div>
      </div>
    </div>

    <!--Carousel controls - prev item-->
    <button
      class="absolute bottom-0 left-0 top-0 z-[1] flex w-[15%] items-center justify-center border-0 bg-none p-0 text-center text-white opacity-50 transition-opacity duration-150 ease-[cubic-bezier(0.25,0.1,0.25,1.0)] hover:text-white hover:no-underline hover:opacity-90 hover:outline-none focus:text-white focus:no-underline focus:opacity-90 focus:outline-none motion-reduce:transition-none"
      type="button">
      <span @click.prevent="gotoPevioustItem()" class="inline-flex items-center justify-center w-10 h-10 rounded-full bg-white/30 dark:bg-gray-800/30 group-hover:bg-white/50 dark:group-hover:bg-gray-800/60 group-focus:ring-4 group-focus:ring-white dark:group-focus:ring-gray-800/70 group-focus:outline-none">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="h-6 w-6">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M15.75 19.5L8.25 12l7.5-7.5" />
        </svg>
      </span>
      <span
        class="!absolute !-m-px !h-px !w-px !overflow-hidden !whitespace-nowrap !border-0 !p-0 ![clip:rect(0,0,0,0)]"
        >Previous</span
      >
    </button>
    <!--Carousel controls - next item-->
    <button
      class="absolute bottom-0 right-0 top-0 z-[1] flex w-[15%] items-center justify-center border-0 bg-none p-0 text-center text-white opacity-50 transition-opacity duration-150 ease-[cubic-bezier(0.25,0.1,0.25,1.0)] hover:text-white hover:no-underline hover:opacity-90 hover:outline-none focus:text-white focus:no-underline focus:opacity-90 focus:outline-none motion-reduce:transition-none"
      type="button">
      <span @click.prevent="gotoNextItem()" class="inline-flex items-center justify-center w-10 h-10 rounded-full bg-white/30 dark:bg-gray-800/60 group-hover:bg-white/50 dark:group-hover:bg-gray-800/60 group-focus:ring-4 group-focus:ring-white dark:group-focus:ring-gray-800/70 group-focus:outline-none">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="h-6 w-6">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M8.25 4.5l7.5 7.5-7.5 7.5" />
        </svg>
      </span>
      <span
        class="!absolute !-m-px !h-px !w-px !overflow-hidden !whitespace-nowrap !border-0 !p-0 ![clip:rect(0,0,0,0)]"
        >Next</span
      >
    </button>
  </div>
</template>

<style scoped></style>