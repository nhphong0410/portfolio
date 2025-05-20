<script setup lang="ts">
import HeroSection from "./sections/HeroSection.vue";
import AboutMe from "./sections/AboutMe.vue";
import TechSet from "./sections/TechSet.vue";
import { onMounted, onUnmounted, provide, ref } from "vue";

const isSmallScreen = ref(false);

const handleResize = () => {
  isSmallScreen.value = window.innerWidth < 768;
};

onMounted(() => {
  handleResize();
  window.addEventListener("resize", handleResize);
});

onUnmounted(() => {
  window.removeEventListener("resize", handleResize);
});

provide("isSmallScreen", isSmallScreen);
</script>

<template>
  <div class="bg-black text-white">
    <main class="w-full max-w-[1280px] mx-auto flex flex-col">
      <HeroSection />
      <AboutMe />
      <TechSet />
    </main>
  </div>
</template>

<style scoped></style>
