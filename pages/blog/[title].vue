<template>
  <div class="container mx-auto px-6 py-12">
    <header class="mb-8">
      <div class="text-sm text-gray-500 mb-2">Features</div>
      <h1 class="text-4xl font-bold text-gray-800 mb-4">{{ title }}</h1>
      <p class="text-gray-500">{{ formattedDate }}</p>
    </header>

    <img
      src="/images/message-apps.jpg"
      alt="Messaging apps in action"
      class="w-full h-auto rounded-lg mb-10 object-cover"
    />

    <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
      <transition name="fade">
        <aside v-if="isSidebarVisible" class="md:col-span-1">
          <div class="border-l-4 border-gray-300 pl-4">
            <ul class="space-y-3 text-sm text-gray-600">
              <li><a href="#" class="hover:text-blue-600">Organize Your Contacts</a></li>
              <li><a href="#" class="hover:text-blue-600">Master the Art of Group Chats</a></li>
              <li><a href="#" class="hover:text-blue-600">Utilize Multimedia Features</a></li>
              <li><a href="#" class="hover:text-blue-600">Be Mindful of Privacy Settings</a></li>
              <li><a href="#" class="hover:text-blue-600">Customize Notifications</a></li>
              <li><a href="#" class="hover:text-blue-600">Embrace Emojis and GIFs</a></li>
              <li><a href="#" class="hover:text-blue-600">Backup Your Conversations</a></li>
              <li><a href="#" class="hover:text-blue-600">Stay Informed About Updates</a></li>
              <li><a href="#" class="hover:text-blue-600">Practice Digital Etiquette</a></li>
            </ul>
          </div>

          <div class="mt-8">
            <h3 class="text-sm font-semibold text-gray-700 mb-2">Share Article</h3>
            <div class="flex space-x-4">
              <a href="#"><img src="/icons/facebook.svg" alt="Facebook" /></a>
              <a href="#"><img src="/icons/twitter.svg" alt="Twitter" /></a>
              <a href="#"><img src="/icons/instagram.svg" alt="Instagram" /></a>
              <a href="#"><img src="/icons/linkedin.svg" alt="LinkedIn" /></a>
            </div>
          </div>
        </aside>
      </transition>

      <article class="md:col-span-3 text-gray-700 space-y-6">
        <p>
          In the fast-paced digital age, messaging apps have become an integral part of our daily communication.
          Whether you're keeping in touch with friends, family, or colleagues, mastering the art of using messaging apps
          effectively can enhance your communication experience. Here are some tips on how to make the most of
          message apps to communicate and share seamlessly:
        </p>

        <h2 class="text-2xl font-semibold">Organize Your Contacts</h2>
        <p>
          Keep your messaging app organized by categorizing your contacts into groups or creating lists.
          This makes it easier to find specific contacts and ensures that your conversations are streamlined
          and efficient.
        </p>

        <h2 class="text-2xl font-semibold">Master the Art of Group Chats</h2>
        <p>
          Group chats are excellent for coordinating plans, discussions, or sharing updates with multiple people.
          However, it&apos;s important to be mindful of the group&apos;s purpose and not overwhelm it with unrelated messages.
          Mute notifications if needed to avoid unnecessary distractions.
        </p>

        <h2 class="text-2xl font-semibold">Utilize Multimedia Features</h2>
        <p>
          Messaging apps offer more than just text communication. Take advantage of multimedia features such as
          sharing photos, videos, and voice messages to add depth to your conversations.
          This can be especially useful for sharing experiences or information in a more engaging way.
        </p>

        <h2 class="text-2xl font-semibold">Be Mindful of Privacy Settings</h2>
        <p>
          Prioritize your privacy by familiarizing yourself with the app's privacy settings. Adjust who can see your status,
          online profile picture, and last seen time according to your preferences. Additionally, consider enabling
          two-factor authentication for an extra layer of security.
        </p>
      </article>
    </div>

    <button
      class="mt-8 bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600"
      @click="toggleSidebar"
    >
      Toggle Sidebar
    </button>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';


const title = ref('');
const isSidebarVisible = ref(true);


const route = useRoute();

onMounted(() => {
  title.value = route.params.title as string;
  console.log(`Loaded article: ${title.value}`);
});


const toggleSidebar = () => {
  isSidebarVisible.value = !isSidebarVisible.value;
};


const formattedDate = computed(() => {
  const date = new Date();
  return date.toLocaleString('en-GB', {
    day: 'numeric',
    month: 'long',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    hour12: true,
  });
});
</script>

<style scoped>
.container {
  max-width: 1100px;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
