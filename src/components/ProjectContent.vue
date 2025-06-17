<script setup lang="ts">
import { ref } from "vue";
import InfiniteCarousel from "./Carousel/InfiniteCarousel.vue";

const projects = ref([
  {
    id: 1,
    title: "Orange Theory Fitness - OrangeBook",
    description:
      "A CRM application, part of the Orange Theory Fitness software ecosystem.",
    technologies: [
      "ReactJS",
      "Redux",
      "Redux Saga",
      "Node.js",
      "Serverless",
      "MySQL",
    ],
    details: [
      "Investigated issues raised by users and customers, provided solutions, and fixed bugs in the application.",
      "Wrote unit tests for both ReactJS and NodeJS source code using Jest to ensure code quality.",
      "Monitored API logs on CloudWatch to identify and resolve issues.",
    ],
    isPersonal: false,
  },
  {
    id: 2,
    title: "Burrito Wallet - Partner Website",
    description:
      "An admin website for the Burrito Wallet's partners to manage their community.",
    technologies: ["NextJS", "Zustand", "Tailwind CSS", "TypeScript"],
    details: [
      "Responsible for building the UI and integrating with the backend API.",
      "Discussed with the designer to clarify the design and make necessary adjustments before implementation.",
      "Collaborated with the backend team to ensure smooth integration and functionality.",
    ],
    isPersonal: false,
  },
  {
    id: 3,
    title: "Neowiz Event - Admin Website",
    description:
      "An admin website for statistics and management of a short-term event run by Neowiz.",
    technologies: ["NextJS", "Redux Toolkit", "Tailwind CSS", "TypeScript"],
    details: [
      "Joined the project to provide urgent support.",
      "Responsible for building the UI and integrating with the backend API, under the direction of the team leader.",
    ],
    isPersonal: false,
  },
]);

const carouselConfig = ref({
  itemsToShow: 1,
  autoplayInterval: 10000,
  showIndicators: true,
  pauseOnHover: true,
});
</script>

<template>
  <InfiniteCarousel
    :items="projects"
    :items-to-show="carouselConfig.itemsToShow"
    :autoplay-interval="carouselConfig.autoplayInterval"
    :show-indicators="carouselConfig.showIndicators"
    :pause-on-hover="carouselConfig.pauseOnHover"
  >
    <template #item="{ item }">
      <div
        class="h-full min-h-[200px] flex flex-col rounded-xl overflow-hidden transition-all bg-gradient-to-tr from-transparent to-[#00a6f466] px-14 pb-8"
      >
        <h3
          class="text-center text-3xl font-semibold py-8 text-shadow-sm text-shadow-sky-800"
        >
          {{ item.title }}
        </h3>
        <div class="flex-1">
          <p v-if="!!item.description" class="italic">{{ item.description }}</p>

          <ul
            v-if="!!item.details && !!item.details.length"
            class="list-disc ml-8 mt-4"
          >
            <li v-for="detail in item.details">{{ detail }}</li>
          </ul>

          <div class="mt-8 flex flex-wrap gap-2">
            <span
              class="block px-4 bg-gray-600 rounded-full"
              v-for="tech in item.technologies"
              >{{ tech }}</span
            >
          </div>
        </div>
      </div>
    </template>
  </InfiniteCarousel>
</template>

<style scoped></style>
