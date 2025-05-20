<script setup lang="ts">
import { computed } from "vue";
import TextButton from "./TextButton.vue";
import IconButton from "./IconButton.vue";

interface Props {
  variant: "text" | "icon";
  color?: string;
  tooltip?: string;
}

const props = defineProps<Props>();
const emit = defineEmits(["click"]);

const buttonProps = computed(() => ({
  color: props.color,
}));

const handleClick = (e: MouseEvent) => {
  emit("click", e);
};
</script>

<template>
  <TextButton
    v-if="props.variant === 'text'"
    v-bind="buttonProps"
    @click="handleClick"
    :class="[$attrs.class]"
  >
    <slot />
  </TextButton>
  <IconButton
    v-else-if="props.variant === 'icon'"
    v-bind="buttonProps"
    :tooltip="props.tooltip"
    @click="handleClick"
    :class="[$attrs.class]"
  >
    <slot />
  </IconButton>
</template>

<style scoped></style>
