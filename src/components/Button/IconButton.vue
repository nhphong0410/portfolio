<script setup lang="ts">
import colors from "tailwindcss/colors.js";
import { ref } from "vue";
interface Props {
  color?: string;
  tooltip?: string;
}
const props = defineProps<Props>();
const emit = defineEmits(["click"]);

const isHover = ref(false);

const handleClick = (e: MouseEvent) => {
  emit("click", e);
};
const handleMouseEnter = () => {
  isHover.value = true;
};
const handleMouseLeave = () => {
  isHover.value = false;
};
</script>

<template>
  <div class="relative">
    <Transition>
      <p
        v-if="isHover && tooltip"
        class="absolute left-1/2 bottom-full -translate-x-1/2 -translate-y-2 w-max bg-gray-300 text-black px-4 italic text-sm font-bold rounded-lg"
      >
        {{ tooltip }}
      </p>
    </Transition>

    <button
      :class="[
        [
          'icon-button relative z-10 p-3 w-12 sm:w-14 md:w-16 aspect-square rounded-lg inline-flex justify-center items-center cursor-pointer bg-transparent overflow-hidden transition-all duration-300',
        ],
        $attrs.class,
      ]"
      :style="{
        '--shadow-color': props.color || colors.sky[500],
      }"
      @click="handleClick"
      @mouseenter="handleMouseEnter"
      @mouseleave="handleMouseLeave"
    >
      <slot />

      <div
        class="absolute -z-10 bottom-0 left-1/2 -translate-x-1/2 translate-y-1/2 rounded-full h-1/2 aspect-square blur-md"
        :style="{ backgroundColor: props.color || colors.sky[500] }"
      ></div>
    </button>
  </div>
</template>

<style scoped>
.icon-button {
  box-shadow: inset 0 -1px 12px 0 var(--shadow-color),
    0 0 1px 0 var(--shadow-color);
}
.icon-button:hover {
  box-shadow: inset 0 -1px 16px 0 var(--shadow-color),
    0 0 4px 0 var(--shadow-color);
  filter: brightness(1.2);
}
.v-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
.v-enter-active {
  transition: all 0.3s ease-in-out;
}
.v-enter-to {
  opacity: 1;
  transform: translateY(0);
}
.v-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.v-leave-active {
  transition: all 0.3s ease-in-out;
}
.v-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>
