<script setup lang="ts">
interface Props {
  title?: string;
  subTitle?: [string | undefined, string | undefined];
}
const props = defineProps<Props>();
</script>

<template>
  <div class="flex items-stretch mt-4">
    <div class="flex flex-col items-center">
      <div
        class="w-5 aspect-square rounded-full bg-transparent border-2 border-sky-500 m-1 z-10"
      ></div>
      <div class="w-0.5 flex-1 bg-sky-500 -mt-1.5 z-0"></div>
    </div>
    <div class="flex-1 flex flex-col gap-0.5">
      <p v-if="props.title" class="text-xl text-center py-1 bg-gradient-to-r from-transparent to-[#00a6f466] rounded-xl">
        {{ props.title }}
      </p>
      <div
        class="text-xl py-1 text-sky-500 flex flex-col sm:flex-row justify-center items-stretch sm:gap-2"
      >
        <p v-if="props.subTitle?.[0]" class="text-center sm:text-right">
          {{ props.subTitle?.[0] }}
        </p>
        <div
          v-if="props.subTitle?.[0] && props.subTitle?.[1]"
          class="w-[2px] rounded-full bg-sky-500 my-1.5 hidden sm:block"
        ></div>
        <p v-if="props.subTitle?.[1]" class="text-center sm:text-left">
          {{ props.subTitle?.[1] }}
        </p>
      </div>
      <div>
        <slot />
      </div>
    </div>
  </div>
</template>
