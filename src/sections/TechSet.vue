<script setup lang="ts">
import SectionTitle from "@/components/SectionTitle.vue";
import colors from "tailwindcss/colors.js";
import {
  programmingLanguages,
  coreStack,
  uiStack,
  databases,
  others,
} from "@/utils/constants";
import TechList from "@/components/TechList.vue";
</script>

<template>
  <section
    id="tech-set"
    class="p-4 md:p-8 w-full mb-12 lg:mt-24 flex flex-col lg:flex-row lg:items-stretch"
  >
    <div class="my-12 lg:flex-1 lg:my-0 order-1 lg:order-3">
      <div class="w-fit mx-auto px-2 py-10 lg:sticky lg:top-1/2">
        <SectionTitle
          primaryText="TECH"
          secondaryText="SET"
          :color="colors.emerald[500]"
        />
      </div>
    </div>
    <div class="lg:flex-1 order-2 flex flex-col gap-8">
      <div>
        <p class="text-lg italic font-semibold text-center">
          Programming languages
        </p>
        <div class="flex gap-2 justify-center items-stretch mt-2">
          <TechList :data="programmingLanguages" />
        </div>
      </div>
      <div>
        <p class="text-lg italic font-semibold text-center">Core stack</p>
        <div class="flex gap-2 justify-center items-stretch mt-2">
          <TechList :data="coreStack" />
        </div>
      </div>
      <div>
        <p class="text-lg italic font-semibold text-center">UI & Styling</p>
        <div class="flex gap-2 justify-center items-stretch mt-2">
          <TechList :data="uiStack" />
        </div>
      </div>
      <div>
        <p class="text-lg italic font-semibold text-center">Databases</p>
        <div class="flex gap-2 justify-center items-stretch mt-2">
          <TechList :data="databases" />
        </div>
      </div>
      <div>
        <p class="text-lg italic font-semibold text-center">Others</p>
        <div class="flex gap-2 justify-center items-stretch mt-2">
          <TechList :data="others" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
