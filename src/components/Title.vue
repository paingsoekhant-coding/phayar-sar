<script setup>
import { ref, onMounted } from "vue";

const title = ref([]);

onMounted(async () => {
  try {
    const response = await fetch("/src/assets/data/data.json");
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    title.value = await response.json();
  } catch (error) {
    console.error("Error fetching JSON data:", error);
  }
});
</script>
<template>
  <div class="basis-1/3 p-4 text-center">
    <div class="flex justify-center">
      <RouterLink :to="{ name: 'home' }">
        <img src="/assets/favicon.png" alt="" class="w-32" />
      </RouterLink>
    </div>
    <div class="">
      <div class="">
        <ul class="">
          <li class="m-6 text-lg" v-for="header in title" :key="header.id">
            <RouterLink
              :to="{ name: 'title', params: { groupId: header.groupId } }"
              >{{ header.title }}</RouterLink
            >
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>