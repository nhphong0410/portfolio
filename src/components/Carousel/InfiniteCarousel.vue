<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount, nextTick } from "vue";

interface CarouselProps {
  items: any[];
  itemsToShow?: number;
  autoplayInterval?: number;
  pauseOnHover?: boolean;
  showNavigation?: boolean;
  showIndicators?: boolean;
}

const props = withDefaults(defineProps<CarouselProps>(), {
  itemsToShow: 1,
  autoplayInterval: 0,
  pauseOnHover: true,
  showNavigation: true,
  showIndicators: true,
});

const current = ref(props.itemsToShow); // Start at first real slide
const isAnimating = ref(false);
const timer = ref<number | null>(null);
const trackRef = ref<HTMLElement | null>(null);
const transitionMs = 400;

const total = computed(() => props.items.length);
const cloneCount = computed(() => Math.min(props.itemsToShow, total.value));

// Slides with clones at both ends
const slides = computed(() => {
  if (!total.value) return [];
  const arr = [];
  // Clones before
  for (let i = total.value - cloneCount.value; i < total.value; i++) {
    arr.push({ ...props.items[i], _clone: true, _idx: i });
  }
  // Originals
  for (let i = 0; i < total.value; i++) {
    arr.push({ ...props.items[i], _clone: false, _idx: i });
  }
  // Clones after
  for (let i = 0; i < cloneCount.value; i++) {
    arr.push({ ...props.items[i], _clone: true, _idx: i });
  }
  return arr;
});

const slideWidth = computed(() => 100 / props.itemsToShow);
const trackStyle = computed(() => ({
  transform: `translateX(-${current.value * slideWidth.value}%)`,
  transition: isAnimating.value
    ? `transform ${transitionMs}ms cubic-bezier(.4,0,.2,1)`
    : "none",
}));

function goTo(idx: number) {
  if (isAnimating.value) return;
  isAnimating.value = true;
  current.value = idx;
}

function goToNext() {
  if (isAnimating.value) return;
  goTo(current.value + 1);
}

function goToPrev() {
  if (isAnimating.value) return;
  goTo(current.value - 1);
}

function onTransitionEnd() {
  isAnimating.value = false;
  // If at clone after last, jump to real first
  if (current.value >= total.value + cloneCount.value) {
    current.value = cloneCount.value;
    disableTransitionOnce();
  }
  // If at clone before first, jump to real last
  if (current.value < cloneCount.value) {
    current.value = total.value + cloneCount.value - 1;
    disableTransitionOnce();
  }
}

function disableTransitionOnce() {
  if (!trackRef.value) return;
  trackRef.value.style.transition = "none";
  // Force reflow
  void trackRef.value.offsetWidth;
  nextTick(() => {
    if (trackRef.value) trackRef.value.style.transition = "";
  });
}

function startAutoplay() {
  if (props.autoplayInterval > 0) {
    timer.value = window.setInterval(() => {
      goToNext();
    }, props.autoplayInterval);
  }
}
function stopAutoplay() {
  if (timer.value) {
    clearInterval(timer.value);
    timer.value = null;
  }
}
function handleMouseEnter() {
  if (props.pauseOnHover) stopAutoplay();
}
function handleMouseLeave() {
  if (props.pauseOnHover) startAutoplay();
}

onMounted(() => {
  startAutoplay();
  if (trackRef.value) {
    trackRef.value.addEventListener("transitionend", onTransitionEnd);
  }
});
onBeforeUnmount(() => {
  stopAutoplay();
  if (trackRef.value) {
    trackRef.value.removeEventListener("transitionend", onTransitionEnd);
  }
});
</script>

<template>
  <div
    class="relative overflow-hidden w-full"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
  >
    <div ref="trackRef" class="flex" :style="trackStyle">
      <div
        v-for="(slide, i) in slides"
        :key="i + '-' + slide._idx + '-' + (slide._clone ? 'c' : 'o')"
        class="flex-shrink-0 px-2"
        :style="{ width: `${slideWidth}%` }"
      >
        <slot name="item" :item="slide" :index="slide._idx" />
      </div>
    </div>
    <div
      v-if="showNavigation && total > props.itemsToShow"
      class="absolute inset-y-0 left-0 right-0 flex justify-between items-center pointer-events-none"
    >
      <button
        @click="goToPrev"
        class="pointer-events-auto bg-white/80 hover:bg-white active:bg-white rounded-full w-10 h-10 flex items-center justify-center shadow-md ml-4 focus:outline-none focus:ring-2 transition-all cursor-pointer"
        aria-label="Previous"
        :disabled="isAnimating"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6 text-gray-800"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
      </button>
      <button
        @click="goToNext"
        class="pointer-events-auto bg-white/80 hover:bg-white active:bg-white rounded-full w-10 h-10 flex items-center justify-center shadow-md mr-4 focus:outline-none focus:ring-2 transition-all cursor-pointer"
        aria-label="Next"
        :disabled="isAnimating"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6 text-gray-800"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M9 5l7 7-7 7"
          />
        </svg>
      </button>
    </div>
    <div
      v-if="showIndicators && total > 1"
      class="absolute bottom-2 left-0 right-0 flex justify-center space-x-2"
    >
      <button
        v-for="i in total"
        :key="'dot-' + i"
        @click="goTo(i - 1 + cloneCount)"
        class="w-2 h-2 rounded-full transition-all focus:outline-none focus:ring-2 cursor-pointer"
        :class="
          (current - cloneCount + total) % total === i - 1
            ? 'bg-blue-600 w-4'
            : 'bg-gray-300 hover:bg-gray-400'
        "
        :disabled="isAnimating"
        :aria-label="`Go to slide ${i}`"
      ></button>
    </div>
  </div>
</template>
