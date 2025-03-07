<script setup>
import data from "@/assets/data/data.json";
</script>

<template>
  <div class="basis-2/3">
    <p>{{ this.$route.params.id }}</p>
    <div class="m-8" v-for="description in data" :key="description.groupId">
      <div class="">
        <!-- <h2 class="text-3xl font-bold">{{ description.title }}</h2> -->
        <div class="" v-for="item in description.data" :key="item.id">
          <ul>
            <li class="mt-6 text-blue-600 font-bold">
              <RouterLink :to="{ name: 'detail', params: { id: item.id } }">{{
                item.title
              }}</RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>