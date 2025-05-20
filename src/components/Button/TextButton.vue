<script setup lang="ts">
interface Props {
  color?: string;
}
const props = defineProps<Props>();
const emit = defineEmits(["click"]);
const handleClick = (e: MouseEvent) => {
  emit("click", e);
};
</script>

<template>
  <button
    :class="[
      [
        'relative z-10 px-10 py-3 rounded-xl bg-transparent overflow-hidden transition-all duration-300 hover:brightness-125 active:brightness-90 cursor-pointer',
      ],
      $attrs.class,
    ]"
    :style="{
      boxShadow: `inset 0 -1px 16px 0px ${props.color}, 0 0 1px 0px ${props.color}`,
    }"
    @click="handleClick"
  >
    <slot />

    <div
      class="absolute -z-10 top-1/2 left-1/2 -translate-x-1/2 rounded-full h-full aspect-square blur-xl"
      :style="{ backgroundColor: props.color }"
    ></div>
  </button>
</template>

<style scoped></style>
