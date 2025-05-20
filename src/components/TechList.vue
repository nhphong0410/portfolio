<script setup lang="ts">
import Button from "./Button/Button.vue";

interface Props {
  data: Array<{
    name?: string;
    iconUrl?: string;
    color?: string;
  }>;
}
const props = defineProps<Props>();
</script>

<template>
  <Button
    v-for="(item, index) in props.data"
    :key="index"
    variant="icon"
    :color="item.color"
    :tooltip="item.name"
  >
    <img :src="item.iconUrl" :alt="item.name" width="100%" height="100%" />
  </Button>
</template>
