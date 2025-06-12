<script setup>
import { items } from "./movies.json";
import Card from "./Card.vue";
import Modal from "./shared/Modal.vue"
import { ref } from 'vue';

const isModalShown = ref(false);
function addNewMovie(){
  isModalShown.value = true;
}

function closeModal(){
  isModalShown.value = false;
}

function createNewMovie($event) {
  isModalShown.value = false;
  items.push($event)
}
</script>

<template>
  <div class="min-h-screen bg-gray-900 p-8">
    <button class="bg-sky-500 hover:bg-sky-700 p-2" @click="addNewMovie()">Add movie</button>
    <div class="flex justify-center content-center flex-wrap">
      <Card v-for="movie in items" :movieProps="movie" />
    </div>
  </div>
  <Modal v-if="isModalShown" @cancel="closeModal()"  @submit="createNewMovie($event)"/>
</template>
