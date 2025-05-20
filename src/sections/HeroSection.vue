<script setup lang="ts">
import Button from "../components/Button/Button.vue";
import ScrollingText from "../components/ScrollingText.vue";
import { EMAIL, PHONE } from "@/utils/constants";
import colors from "tailwindcss/colors.js";
import { inject } from "vue";
import { useToast } from "vue-toast-notification";

const $toast = useToast();
const isSmallScreen = inject<{ value: boolean }>("isSmallScreen");

const goToAboutMe = () => {
  window.location.href = "#about-me";
};
const goToTechSet = () => {
  window.location.href = "#tech-set";
};
const handleEmailClick = async (e: MouseEvent) => {
  e.preventDefault();
  try {
    await navigator.clipboard.writeText(EMAIL);
    $toast.open({
      message: "Email copied to clipboard",
      type: "success",
      position: isSmallScreen?.value ? "top" : "top-right",
      duration: 1000,
    });
  } catch {}
};
const handlePhoneClick = async (e: MouseEvent) => {
  e.preventDefault();
  try {
    await navigator.clipboard.writeText(PHONE);
    $toast.open({
      message: "Phone number copied to clipboard",
      type: "success",
      position: isSmallScreen?.value ? "top" : "top-right",
      duration: 1000,
    });
  } catch {}
};
</script>

<template>
  <section
    id="hero-section"
    class="w-full h-screen p-4 md:p-8 flex flex-col justify-center items-center gap-4"
  >
    <div
      class="fugaz-text relative flex-1 flex flex-col justify-center items-center gap-4 w-full z-0"
    >
      <p class="text-2xl md:text-4xl text-center">&#128075; Hi, I am</p>
      <p
        class="text-4xl md:text-6xl lg:text-7xl text-center text-sky-500 text-shadow-sm text-shadow-sky-300"
      >
        Nguyen Hong Phong
      </p>
      <p class="text-2xl md:text-4xl text-center">Junior Frontend Developer</p>

      <div
        class="absolute w-40 aspect-square bg-sky-500 blur-3xl opacity-50 -z-10"
      ></div>
      <div class="absolute top-[10%] left-[5%] sm:left-1/6 bounce-button">
        <Button
          variant="text"
          :color="colors.sky[500]"
          class="w-40 md:w-48"
          @click="goToAboutMe"
        >
          <p class="fugaz-text text:lg md:text-xl text-sky-500 truncate">
            About me
          </p>
        </Button>
      </div>
      <div class="absolute bottom-[10%] right-[5%] sm:right-1/6 bounce-button">
        <Button
          variant="text"
          :color="colors.emerald[500]"
          class="w-40 md:w-48"
          @click="goToTechSet"
        >
          <p class="fugaz-text text:lg md:text-xl text-emerald-500 truncate">
            Tech set
          </p>
        </Button>
      </div>
    </div>
    <div class="flex flex-col md:flex-row md:justify-center gap-4 w-full">
      <div class="flex gap-4 justify-start md:justify-end items-center">
        <Button
          variant="icon"
          :color="colors.sky[500]"
          @click="handleEmailClick"
        >
          <img
            src="/assets/svgs/svg-mail.svg"
            alt="email"
            width="100%"
            height="100%"
          />
        </Button>
        <div
          class="flex-1 md:flex-none truncate cursor-pointer text-lg"
          @click="handleEmailClick"
        >
          <ScrollingText>
            {{ EMAIL }}
          </ScrollingText>
        </div>
      </div>
      <div class="flex gap-4 justify-start items-center">
        <Button
          variant="icon"
          :color="colors.sky[500]"
          @click="handlePhoneClick"
        >
          <img
            src="/assets/svgs/svg-phone.svg"
            alt="phone"
            width="100%"
            height="100%"
          />
        </Button>
        <div
          class="flex-1 md:flex-none truncate cursor-pointer text-lg"
          @click="handlePhoneClick"
        >
          <ScrollingText>
            {{ PHONE }}
          </ScrollingText>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.fugaz-text {
  font-family: "Fugaz One", sans-serif;
}

.bounce-button {
  animation: bounce 10s ease-in-out infinite;
}
.bounce-button:hover {
  animation-play-state: paused;
}

@keyframes bounce {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
