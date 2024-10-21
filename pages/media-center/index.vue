<template>
  <div :class="container" class="py-20 space-y-20">
    <div class="space-y-10">
      <div class="flex flex-col gap-2.5">
        <h1 class="text-[#113912] text-3xl md:text-4xl">MEDIA Center</h1>
        <p class="text-[#1C6220] text-lg sm:text-xl">
          Discover Our Latest News, Updates, and Visual Highlights
        </p>
      </div>

      <div class="flex flex-col gap-2.5">
        <div class="relative flex flex-col h-[500px] w-full justify-end">
          <video
            src="/metro_motion.webm"
            autoplay
            muted
            class="absolute top-0 left-0 size-full object-cover"
          ></video>
          <div class="p-5 bg-black/20 backdrop-blur-sm gap-2.5">
            <p class="text-white text-base md:text-lg font-noto">
              Powering the Future
            </p>
            <h2
              class="text-white text-2xl md:text-3xl font-main font-semibold md:font-bold"
            >
              Next-gen EVs for a cleaner tomorrow.
            </h2>
          </div>
        </div>
      </div>
    </div>
    <div class="space-y-10">
      <div class="flex flex-col gap-2.5">
        <h1 class="text-[#113912] text-3xl md:text-4xl">Latest News</h1>
        <p class="text-[#1C6220] text-lg sm:text-xl">
          Stay Informed with the Latest News and Updates
        </p>
      </div>

      <div class="flex flex-col items-center gap-2.5">
        <MediaNews
          class="w-full"
          :title="news[news.length - 1].title"
          :description="news[news.length - 1].description"
          :content="news[news.length - 1].content"
          :slug="news[news.length - 1].slug"
          :image="news[news.length - 1].image"
        />
        <div class="flex w-full">
          <Swiper
            :modules="[SwiperAutoplay, SwiperNavigation]"
            class="size-full"
            :direction="'horizontal'"
            :space-between="0"
            :navigation="true"
            :slidesPerView="1"
            :loop="true"
            :grabCursor="true"
            :autoplay="{
              delay: 10000,
              disableOnInteraction: false,
            }"
            @autoplayTimeLeft="onAutoplayTimeLeft"
            :breakpoints="{
              '640': {
                slidesPerView: 2,
                spaceBetween: 10,
              },
            }"
          >
            <SwiperSlide
              v-for="(newsItem, index) in news"
              :key="index"
              class="size-full"
            >
              <MediaNews
                :title="newsItem.title"
                :description="newsItem.description"
                :content="newsItem.content"
                :slug="newsItem.slug"
                :image="newsItem.image"
              />
            </SwiperSlide>
            <template #container-end>
              <div class="autoplay-progress">
                <svg class="size-6" viewBox="0 0 48 48" ref="progressCircle">
                  <circle cx="24" cy="24" r="20"></circle>
                </svg>
                <span ref="progressContent"></span>
              </div>
            </template>
          </Swiper>
        </div>
      </div>
    </div>
    <div class="space-y-10">
      <div class="flex flex-col gap-2.5">
        <h1 class="text-[#113912] text-3xl md:text-4xl">Gallery</h1>
        <p class="text-[#1C6220] text-lg sm:text-xl">
          Explore Our Collection of Moments and Visual Highlights
        </p>
      </div>

      <div class="flex flex-col items-center gap-2.5">
        <div
          class="relative grid grid-flow-row-dense justify-center w-full gap-2.5 overflow-hidden transition-all duration-300 ease-in"
          :style="`height:${gallerySize}px`"
        >
          <MediaItem
            v-for="(blog, index) in blogs"
            class="col-span-12"
            :class="
              index == 0 || index % 3 == 0 ? 'md:col-span-12' : 'md:col-span-6'
            "
            :title="blog.title"
            :description="blog.description"
            :slug="blog.slug"
            :content="blog.content"
            :date="blog.date"
            :minutes-read="blog.minutesRead"
            :tags="blog.tags"
            :image="blog.image"
          />
        </div>

        <button
          @click="loadMore"
          class="mt-5 flex justify-center items-center py-3 px-8 text-white bg-[#1C6220] hover:bg-[#113912] gap-2.5 w-fit disabled:opacity-10"
          :disabled="isLoading"
        >
          Load More
          <ArrowDownIcon
            v-if="!isLoading"
            class="size-6 text-white font-main"
          />
          <ArrowPathIcon class="animate-spin size-6 mx-auto" v-if="isLoading" />
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ArrowDownIcon, ArrowPathIcon } from "@heroicons/vue/20/solid";
import { Swiper, SwiperSlide } from "swiper/vue";
import { SwiperAutoplay, SwiperNavigation } from "#imports";
import type { NewsItem } from "~/types/types";
const { container } = useTailwindConfig();
const gallerySize = ref();
const isLoading = ref(false);
const progressCircle = ref();
const progressContent = ref<HTMLElement | null>(null);

gallerySize.value = 1020;

const onAutoplayTimeLeft = (s: any, time: number, progress: any) => {
  if (progressCircle.value) {
    progressCircle.value.style.setProperty("--progress", 1 - progress);
  }
  if (progressContent.value) {
    progressContent.value.textContent = `${Math.ceil(time / 1000)}s`;
  }
};

useSeoMeta({
  title: "Media Center",
  ogTitle: "Media Center",
  description:
    "Metropolitan Electric Limited is at the forefront of revolutionizing the Electric Vehicle (EV) industry across Africa.",
  ogDescription:
    "Metropolitan Electric Limited is at the forefront of revolutionizing the Electric Vehicle (EV) industry across Africa.",
  ogImage: "https://metropolitanelectricng.com/logo.svg",
  twitterCard: "summary_large_image",
});

const loadMore = () => {
  isLoading.value = true;
  setTimeout(() => {
    gallerySize.value = gallerySize.value + 1020;
    isLoading.value = false;
    console.log(gallerySize.value);
  }, 500);
};

defineProps<{ news: NewsItem[] }>();

const blogs = [
  {
    title: "Sustainable Mobility: The Future of Urban Transportation",
    description:
      "Exploring strategies for eco-friendly and efficient urban transportation in growing cities.",
    content:
      "As cities grow and populations increase, the need for sustainable mobility solutions is more urgent than ever. This blog explores various strategies to make urban transportation eco-friendly and efficient.",
    tags: ["sustainability", "urban mobility", "green transportation"],
    image: "pause",
    date: "2024-10-01",
    slug: "sustainable-mobility-urban-transportation",
    minutesRead: 7,
  },
  {
    title: "Top 5 Bottle Recycling Hacks to Try at Home",
    description:
      "Creative and fun ways to recycle plastic bottles and contribute to environmental sustainability.",
    content:
      "Recycling bottles doesn't have to be boring! Learn five creative ways to repurpose your old plastic bottles while helping the environment.",
    tags: ["recycling", "DIY", "eco-friendly"],
    image: "pause",
    date: "2024-09-25",
    slug: "top-bottle-recycling-hacks",
    minutesRead: 5,
  },
  {
    title: "How to Set Up an Electric Vehicle Charging Station at Home",
    description:
      "A step-by-step guide to setting up your own electric vehicle charging station at home.",
    content:
      "With more people adopting electric vehicles, setting up a home charging station is becoming a necessity. This guide walks you through the process step-by-step.",
    tags: ["EV charging", "electric vehicles", "sustainability"],
    image: "pause",
    date: "2024-09-18",
    slug: "setup-ev-charging-station",
    minutesRead: 8,
  },
  {
    title: "The Economic Benefits of Recycling Plastics",
    description:
      "How recycling plastics boosts the economy by creating jobs and reducing business costs.",
    content:
      "Recycling plastics doesn't just save the environment – it can also boost the economy. Learn how recycling initiatives create jobs and reduce costs for businesses.",
    tags: ["recycling", "economy", "sustainability"],
    image: "pause",
    date: "2024-09-10",
    slug: "economic-benefits-recycling",
    minutesRead: 6,
  },
  {
    title: "Why Renewable Energy is the Key to a Greener Future",
    description:
      "The role of renewable energy sources in reducing carbon emissions and combating climate change.",
    content:
      "This article explores how renewable energy sources, like solar and wind power, can significantly reduce carbon emissions and combat climate change.",
    tags: ["renewable energy", "sustainability", "green future"],
    image: "pause",
    date: "2024-08-30",
    slug: "renewable-energy-greener-future",
    minutesRead: 9,
  },
  {
    title: "Understanding the Lifecycle of PET Plastics",
    description:
      "A deep dive into the lifecycle of PET plastics, from production to recycling.",
    content:
      "From production to recycling, PET plastics have a unique lifecycle. Discover how these materials can be transformed into new products through proper recycling techniques.",
    tags: ["PET plastics", "recycling", "materials"],
    image: "pause",
    date: "2024-08-25",
    slug: "lifecycle-of-pet-plastics",
    minutesRead: 4,
  },
  {
    title: "5 Steps to Building a Sustainable Business Model",
    description:
      "Essential steps to integrate eco-friendly practices into your business operations.",
    content:
      "Looking to make your business more sustainable? This guide covers five essential steps to integrate eco-friendly practices into your company's core operations.",
    tags: ["business", "sustainability", "green business"],
    image: "pause",
    date: "2024-08-12",
    slug: "steps-sustainable-business-model",
    minutesRead: 7,
  },
  {
    title: "How Electric Vehicles Are Revolutionizing Fleet Management",
    description:
      "Discover how electric vehicles are transforming the way companies manage their fleets.",
    content:
      "Electric vehicles (EVs) are changing the game for fleet managers. Find out how EVs can reduce costs and improve efficiency for corporate fleets.",
    tags: ["electric vehicles", "fleet management", "sustainability"],
    image: "pause",
    date: "2024-07-28",
    slug: "ev-fleet-management-revolution",
    minutesRead: 6,
  },
  {
    title: "The Importance of Local Manufacturing in Sustainable Development",
    description:
      "How local manufacturing contributes to sustainable development and economic growth.",
    content:
      "Local manufacturing plays a vital role in reducing emissions and supporting economic growth. Learn how sustainable practices are being integrated into manufacturing industries.",
    tags: ["local manufacturing", "sustainable development", "green economy"],
    image: "pause",
    date: "2024-07-15",
    slug: "importance-local-manufacturing",
    minutesRead: 8,
  },
  {
    title: "How Bottle Caps Can Be Recycled for a Cleaner Environment",
    description:
      "Learn why recycling bottle caps can make a big difference in environmental conservation.",
    content:
      "Many people overlook bottle caps in recycling efforts. This article explains how these small items can make a big impact when recycled properly.",
    tags: ["recycling", "bottle caps", "environment"],
    image: "pause",
    date: "2024-07-02",
    slug: "recycling-bottle-caps",
    minutesRead: 4,
  },
  {
    title: "The Role of Education in Promoting Environmental Stewardship",
    description:
      "Explore how environmental education initiatives are shaping eco-conscious communities.",
    content:
      "Environmental education is key to creating a more sustainable future. Discover how education initiatives are shaping eco-conscious communities.",
    tags: ["education", "environmental stewardship", "sustainability"],
    image: "pause",
    date: "2024-06-21",
    slug: "role-education-environmental-stewardship",
    minutesRead: 7,
  },
  {
    title: "How Renewable Energy Can Power the Next Generation of Smart Cities",
    description:
      "Discover the role of renewable energy in building smarter, more sustainable cities.",
    content:
      "Smart cities are on the rise, and renewable energy is a crucial component. Learn how integrating green energy solutions is key to building smarter, sustainable cities.",
    tags: ["smart cities", "renewable energy", "sustainability"],
    image: "pause",
    date: "2024-06-15",
    slug: "renewable-energy-smart-cities",
    minutesRead: 9,
  },
  {
    title: "Recycling Initiatives Around the World: What We Can Learn",
    description:
      "Explore successful global recycling programs and the lessons they offer for local initiatives.",
    content:
      "From Sweden to Japan, countries across the globe are setting benchmarks in recycling. This blog explores various global recycling programs and what we can learn from them.",
    tags: ["recycling", "global initiatives", "sustainability"],
    image: "pause",
    date: "2024-06-03",
    slug: "global-recycling-initiatives",
    minutesRead: 8,
  },
  {
    title: "The Growing Demand for Electric Vehicles in Africa",
    description:
      "An in-depth look at why Africa is experiencing a surge in electric vehicle adoption.",
    content:
      "Africa is seeing a surge in the demand for electric vehicles. Explore the factors contributing to this growing trend and its impact on the continent's future.",
    tags: ["electric vehicles", "Africa", "sustainable mobility"],
    image: "pause",
    date: "2024-05-28",
    slug: "electric-vehicles-demand-africa",
    minutesRead: 6,
  },
  {
    title: "How to Reduce Plastic Waste in Your Daily Life",
    description:
      "Simple tips to cut down on plastic consumption and contribute to a cleaner environment.",
    content:
      "Reducing plastic waste starts at home. Here are some simple and effective ways you can cut down on your plastic consumption and help protect the environment.",
    tags: ["plastic waste", "recycling", "eco-friendly habits"],
    image: "pause",
    date: "2024-05-15",
    slug: "reduce-plastic-waste-daily-life",
    minutesRead: 5,
  },
];
</script>
<style>
.autoplay-progress {
  position: absolute;
  right: 16px;
  top: 16px;
  z-index: 10;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  color: #10b526;
}

.autoplay-progress svg {
  --progress: 0;
  position: absolute;
  left: 0;
  top: 0px;
  z-index: 10;
  width: 100%;
  height: 100%;
  stroke-width: 4px;
  stroke: #10b526;
  fill: none;
  stroke-dashoffset: calc(125.6px * (1 - var(--progress)));
  stroke-dasharray: 125.6;
  transform: rotate(-90deg);
}

.swiper-button-next,
.swiper-button-prev {
  width: 32px;
  height: 32px;
  background-color: #0a8210;
  border-radius: 50%;
  box-shadow: 4px 10px 10.770329614269007px -3.75px rgba(0, 0, 0, 0.0625);
}

.swiper-button-next::after,
.swiper-button-prev::after {
  font-weight: bold;
  font-size: 18px;
  left: 16px;
  color: white;
}
</style>
