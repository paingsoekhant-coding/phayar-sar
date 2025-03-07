<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const dataJson = ref(null);
const oneJson = ref(null);
const route = useRoute();

const fetchData = async () => {
  try {
    const dataResponse = await fetch("/assets/data/data.json");
    dataJson.value = await dataResponse.json();
    if (route.params.groupId && route.params.id) {
      const oneResponse = await fetch(
        `/assets/data/${route.params.groupId}/${route.params.id}.json`
      );
      oneJson.value = await oneResponse.json();
    }
  } catch (error) {
    console.error("Error fetching JSON data:", error);
  }
};

onMounted(() => {
  fetchData();
});
</script>

<template>
  <div class="basis-2/3 mt-10 text-wrap">
    <RouterLink
      :to="{ name: 'title' }"
      class="bg-black rounded-lg text-white w-24 p-2"
      >Back</RouterLink
    >
    <h2 v-if="oneJson" class="text-3xl font-bold mt-8">{{ oneJson.title }}</h2>

    <ul>
      <li v-if="oneJson" class="mt-8 font-bold mb-14">
        {{ oneJson.content }}
      </li>
    </ul>
  </div>
</template>