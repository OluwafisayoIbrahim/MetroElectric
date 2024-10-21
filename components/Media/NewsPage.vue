<template>
  <div class="flex flex-col gap-20">
    <div class="relative w-full h-[60vh]">
      <img class="size-full object-cover" src="/bgImage.png" alt="News Image" />
    </div>

    <div class="w-full space-y-2.5" :class="container">
      <p class="text-lg text-[#1C6220]">{{ title }}</p>
      <div
        class="grid grid-cols-12 grid-flow-row-dense justify-center w-full gap-20"
      >
        <div class="flex flex-col col-span-9 gap-5">
          <div class="flex flex-col gap-2.5">
            <h1 class="text-3xl">{{ description }}</h1>
            <p class="px-2.5 py-1.5 text-xs bg-[#1C6220]/10 w-fit">
              {{ date }}
            </p>
          </div>
          <p id="content1" class="text-lg">{{ content }}</p>
          <div id="featured-image" class="h-[500px] w-full">
            <img class="w-full object-cover" src="/bgImage.png" alt="" />
          </div>
          <p id="content2" class="text-lg">{{ content }}</p>
        </div>
        <div class="col-span-3">
          <h1 class="text-2xl">Related News</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const { container } = useTailwindConfig();
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
  content: {
    type: String,
    required: true,
  },
  image: {
    type: String,
    required: true,
  },
  slug: {
    type: String,
    required: true,
  },
  date: {
    type: String,
    required: true,
  },
});
</script>
