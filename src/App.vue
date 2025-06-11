<script setup>
import { items } from "./movies.json";
import Card from "./Card.vue";

</script>

<template>
  <div class="min-h-screen bg-gray-900 p-8">
    <div class="flex justify-center content-center">
      <Card v-for="movie in items" :movieProps="movie" />
    </div>
  </div>
</template>
