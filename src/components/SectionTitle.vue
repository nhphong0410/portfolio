<script setup lang="ts">
import colors from "tailwindcss/colors.js";
interface Props {
  primaryText: string;
  secondaryText: string;
  color?: string;
}
const props = defineProps<Props>();
</script>

<template>
  <p
    class="primary-text text-right text-6xl font-bold lg:text-8xl leading-8 lg:leading-10 -translate-x-1 tracking-wider"
  >
    {{ props.primaryText?.toLocaleUpperCase() }}
  </p>
  <p
    class="secondary-text text-right text-6xl font-bold lg:text-8xl leading-8 lg:leading-10 translate-x-1 tracking-wider"
    :style="{ '--text-color': props.color || colors.sky[500] }"
  >
    {{ props.secondaryText?.toLocaleUpperCase() }}
  </p>
</template>

<style scoped>
.primary-text,
.secondary-text {
  font-family: "Fugaz One", sans-serif;
}

.secondary-text {
  color: transparent;
  -webkit-text-stroke: 1px var(--text-color);
}
</style>
