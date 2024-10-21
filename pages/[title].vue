<template>
  <div>
    <div class="p-5 sm:p-10">
      <Service
        v-if="selectedCard"
        :image="selectedCard.image"
        :title="selectedCard.title"
        :description="selectedCard.description"
      />
    </div>
    <div class="bg-[#1C6220] p-5 sm:p-10">
      <div class="py-32 mx-auto">
        <div class="flex flex-col gap-5" :class="container">
          <p
            class="text-white text-3xl sm:text-4xl font-semibold sm:font-medium"
          >
            We Would Love To Hear From You
          </p>
          <p class="text-white text-lg font-serif max-w-2xl">
            Feel free to give us a call or send us an email with any questions
            or comments you have.
          </p>
          <NuxtLink
            to="/#contact"
            class="px-8 py-2.5 text-white border-2 border-white bg-[#1C6220] hover:bg-[#113912] hover:border-transparent w-fit font-semibold transition-colors duration-200"
            >Get In Touch</NuxtLink
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { Card } from "~/types/types.js";
const props = defineProps<{ data: Card[] }>();

const { container } = useTailwindConfig();
const route = useRoute();

const { title } = route.params;

const selectedCard = ref();

onMounted(() => {
  const card = props.data.find((card: Card) => card.link === title);
  selectedCard.value = card;
});

useSeoMeta({
  title: selectedCard.value
    ? selectedCard.value.title
    : "Metropolitan Electric",
  ogTitle: selectedCard.value
    ? selectedCard.value.title
    : "Metropolitan Electric",
  description:
    "Metropolitan Electric Limited is at the forefront of revolutionizing the Electric Vehicle (EV) industry across Africa.",
  ogDescription:
    "Metropolitan Electric Limited is at the forefront of revolutionizing the Electric Vehicle (EV) industry across Africa.",
  ogImage: selectedCard.value
    ? selectedCard.value.image
    : "https://metropolitanelectricng.com/logo.svg",
  twitterCard: "summary_large_image",
});
</script>
