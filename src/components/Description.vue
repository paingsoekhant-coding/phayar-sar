<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";

const data = ref([]);
const route = useRoute();
onMounted(async () => {
  try {
    const response = await fetch("/src/assets/data/data.json");
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    data.value = await response.json();
  } catch (error) {
    console.error("Error fetching JSON data:", error);
  }
});
</script>
<template>
  <div class="basis-2/3">
    <div class="m-8" v-for="description in data" :key="description.groupId">
      <div class="" v-if="description.groupId == route.params.groupId">
        <h2 class="text-3xl font-bold">{{ description.title }}</h2>
        <div class="" v-for="item in description.data" :key="item.id">
          <ul>
            <li class="mt-8 text-blue-600 font-bold">
              <RouterLink
                :to="{
                  name: 'detail',
                  params: { id: item.id, groupId: item.groupId },
                }"
                >{{ item.title }}</RouterLink
              >
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>