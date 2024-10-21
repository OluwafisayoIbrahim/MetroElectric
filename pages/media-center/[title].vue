<template>
  <div class="w-full">
    <MediaNewsPage
      v-if="currentNews"
      :title="currentNews.title"
      :description="currentNews.description"
      :content="currentNews.content"
      :image="currentNews.image"
      :slug="currentNews.slug"
      :date="currentNews.date"
    />
  </div>
</template>

<script lang="ts" setup>
import type { NewsItem } from "~/types/types.js";
const props = defineProps<{ news: NewsItem[] }>();

const route = useRoute();

const { title } = route.params;

const currentNews = ref();

onMounted(() => {
  const news = props.news.find((news: NewsItem) => news.slug === title);
  currentNews.value = news;
});
</script>
