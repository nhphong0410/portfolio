<script setup lang="ts">
import { ref } from 'vue';
import InfiniteCarousel from './InfiniteCarousel.vue';

// Demo items for the carousel
const carouselItems = ref([
  {
    id: 1,
    title: 'First Slide',
    description: 'This is the first slide content',
    image: 'https://via.placeholder.com/800x400/3B82F6/FFFFFF?text=Slide+1',
    bgColor: 'bg-blue-500'
  },
  {
    id: 2,
    title: 'Second Slide',
    description: 'This is the second slide content',
    image: 'https://via.placeholder.com/800x400/10B981/FFFFFF?text=Slide+2',
    bgColor: 'bg-green-500'
  },
  {
    id: 3,
    title: 'Third Slide',
    description: 'This is the third slide content',
    image: 'https://via.placeholder.com/800x400/F59E0B/FFFFFF?text=Slide+3',
    bgColor: 'bg-yellow-500'
  },
  {
    id: 4,
    title: 'Fourth Slide',
    description: 'This is the fourth slide content',
    image: 'https://via.placeholder.com/800x400/EF4444/FFFFFF?text=Slide+4',
    bgColor: 'bg-red-500'
  },
  {
    id: 5,
    title: 'Fifth Slide',
    description: 'This is the fifth slide content',
    image: 'https://via.placeholder.com/800x400/8B5CF6/FFFFFF?text=Slide+5',
    bgColor: 'bg-purple-500'
  }
]);

// Different configuration examples
const singleItemAutoplay = ref({
  itemsToShow: 1,
  autoplayInterval: 3000,
  showIndicators: true,
  pauseOnHover: true
});

const multipleItems = ref({
  itemsToShow: 3,
  autoplayInterval: 0,
  showIndicators: false,
  pauseOnHover: true
});
</script>

<template>
  <div class="space-y-12 py-8">
    <!-- Example 1: Single item with autoplay -->
    <div>
      <h2 class="text-xl font-bold mb-4">Single Item Carousel with Autoplay</h2>      <InfiniteCarousel 
        :items="carouselItems" 
        :autoplay-interval="singleItemAutoplay.autoplayInterval"
        :items-to-show="singleItemAutoplay.itemsToShow"
        :show-indicators="singleItemAutoplay.showIndicators"
        :pause-on-hover="singleItemAutoplay.pauseOnHover"
      >
        <template #item="{ item }">
          <div class="relative h-64 rounded-lg overflow-hidden shadow-lg">
            <img :src="item.image" alt="" class="w-full h-full object-cover" />
            <div class="absolute inset-0 flex flex-col justify-end p-6 bg-gradient-to-t from-black/70 to-transparent">
              <h3 class="text-xl font-bold text-white">{{ item.title }}</h3>
              <p class="text-white/90">{{ item.description }}</p>
            </div>
          </div>
        </template>
      </InfiniteCarousel>
    </div>

    <!-- Example 2: Multiple items without autoplay -->
    <div>
      <h2 class="text-xl font-bold mb-4">Multiple Items Carousel</h2>      <InfiniteCarousel 
        :items="carouselItems" 
        :items-to-show="multipleItems.itemsToShow"
        :show-indicators="multipleItems.showIndicators"
        :pause-on-hover="multipleItems.pauseOnHover"
      >
        <template #item="{ item }">
          <div class="h-48 mx-2 rounded-lg overflow-hidden shadow-md hover:shadow-xl transition-shadow duration-300">
            <div :class="[item.bgColor, 'h-full flex flex-col justify-center items-center text-white p-4']">
              <h3 class="text-lg font-semibold">{{ item.title }}</h3>
              <p class="text-sm text-center mt-2">{{ item.description }}</p>
            </div>
          </div>
        </template>
      </InfiniteCarousel>
    </div>
  </div>
</template>
