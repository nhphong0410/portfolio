<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, computed } from "vue";

const scrollText = ref<HTMLElement | null>(null);
const direction = ref<"forwards" | "backwards">("forwards");
const animationDuration = ref(0);
const isPaused = ref(false);

const animationStyle = computed(() => {
  if (!animationDuration.value) return {};
  const parent = scrollText.value?.parentElement;
  const text = scrollText.value;
  let scrollDistance = 0;
  if (parent && text) {
    scrollDistance = parent.offsetWidth - text.scrollWidth;
  }
  return {
    "--scroll-distance": `${scrollDistance}px`,
    animation: `scroll-x ${animationDuration.value}s linear 1s infinite ${
      direction.value === "backwards" ? "reverse" : ""
    }`.trim(),
  };
});

function toggleDirection() {
  direction.value = direction.value === "forwards" ? "backwards" : "forwards";
}

function pauseAnimation() {
  isPaused.value = true;
  if (scrollText.value) {
    scrollText.value.style.animationPlayState = "paused";
  }
}

function resumeAnimation() {
  isPaused.value = false;
  if (scrollText.value) {
    scrollText.value.style.animationPlayState = "running";
  }
}

function handleResize() {
  const parent = scrollText.value?.parentElement;
  const text = scrollText.value;
  if (parent && text) {
    const parentWidth = parent.offsetWidth;
    const textWidth = text.scrollWidth;
    if (textWidth > parentWidth) {
      animationDuration.value = Math.max(
        2,
        Math.round((textWidth - parentWidth) / 10)
      );
    } else {
      animationDuration.value = 0;
    }
  }
}

onMounted(() => {
  handleResize();
  window.addEventListener("resize", handleResize);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", handleResize);
});
</script>

<template>
  <div class="w-full overflow-hidden relative">
    <p
      ref="scrollText"
      class="w-fit whitespace-nowrap scrolling-text"
      :style="animationStyle"
      @animationiteration="toggleDirection"
      @mouseenter="pauseAnimation"
      @mouseleave="resumeAnimation"
    >
      <slot />
    </p>
  </div>
</template>

<style>
@keyframes scroll-x {
  0% {
    transform: translateX(0);
  }
  10% {
    transform: translateX(0);
  }
  90% {
    transform: translateX(calc(var(--scroll-distance, 0px)));
  }
  100% {
    transform: translateX(calc(var(--scroll-distance, 0px)));
  }
}
.scrolling-text {
  display: inline-block;
  will-change: transform;
}
</style>
