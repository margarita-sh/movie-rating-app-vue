<script setup>
import { items } from "./movies.json";
import Card from "./Card.vue";
import Modal from "./shared/Modal.vue"
import { ref } from 'vue';

const isModalShown = ref(false);
const selectedMovie = ref(null);
const movies = ref(items);
function addNewMovie(){
  selectedMovie.value = null;
  isModalShown.value = true;
}

function closeModal(){
  isModalShown.value = false;
}

function createNewMovie($event) {
  isModalShown.value = false;
  if (selectedMovie.value) {
  const selectedInd = movies.value.findIndex(item => item.id === selectedMovie.value.id);
  if (selectedInd !== -1) {
    movies.value.splice(selectedInd, 1, { ...$event, id: selectedMovie.value.id });
  }
} else {
  const idx = movies.value.length + 1;
  movies.value.push({ ...$event, id: idx });
}
  selectedMovie.value = null;
}

function editMovie($event) {
  isModalShown.value = true;
  selectedMovie.value = $event;
}

function removeMovie($event) {
    const result =  movies.value.filter(movie=> movie.id !== $event.id);
    movies.value = result;
}
</script>

<template>
  <div class="min-h-screen bg-gray-900 p-8">
    <button class="bg-sky-500 hover:bg-sky-700 p-2" @click="addNewMovie()">Add movie</button>
    <div class="flex justify-center content-center flex-wrap">
      <Card v-for="movie in movies" :movieProps="movie" @edit="editMovie(movie)" @remove="removeMovie(movie)"/>
    </div>
  </div>
  <Modal v-if="isModalShown" @cancel="closeModal()" @submit="createNewMovie($event)" :movie="selectedMovie"/>
</template>
