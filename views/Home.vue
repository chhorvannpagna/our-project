<template>
  <div class="p-8 pb-0 text-indigo-500">
    <h1 class="text-4xl font-bold mb-4">Random Meals</h1>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosClient from "../axiosClient.js";
import Meals from "../components/Meals.vue";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    const { data } = await axiosClient.get("random.php");
    if (data.meals && data.meals.length) {
      meals.value.push(data.meals?.[0]);
    }
  }
});

</script>