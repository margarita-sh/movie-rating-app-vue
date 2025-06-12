<script setup>
import { StarIcon } from "@heroicons/vue/24/solid";
import { ref } from 'vue';

const { movieProps } = defineProps({
  movieProps: {
    type: Object,
    required: true
  }
})

const currentIndx = ref(movieProps.rating);

function setStars($event) {
  currentIndx.value = $event;
}
const disabledState = 'cursor-not-allowed text-gray-300';
const enabledState = 'cursor-pointer';
</script>

<template>
  <div :id="movieProps.id" class="bg-white rounded-lg shadow-md overflow-hidden m-4 w-96 h-auto">
    <div class="relative">
      <img :src="movieProps.image" alt="movie poster" class="w-full h-96 object-cover" />
      <div class="absolute top-0 right-0 w-16 h-16">
        <div class="relative w-full h-full flex items-center justify-center">
          <StarIcon class="text-yellow-400 w-full h-full" />
          <span class="absolute text-yellow-800 font-bold text-sm">
            {{ currentIndx > 0 ? currentIndx : "-" }}
          </span>
        </div>
      </div>
    </div>
    <div class="p-4">
      <h3 class="text-lg font-semibold text-gray-900 mb-2">{{ movieProps.name }}</h3>
      <div class="flex flex-wrap gap-2 mb-2">
        <span v-for="(genre, index) in movieProps.genres" :key="index"
          class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded-full">
          {{ genre }}
        </span>
      </div>
      <p class="text-sm text-gray-700 mb-3">{{ movieProps.description }}</p>
      <div class="flex items-center">
        <span class="text-sm text-gray-600 mr-2">Rating: ({{ (currentIndx) > 0 ? (currentIndx) : "-" }}/5)</span>
        <StarIcon v-for="i in 5" :key="i" class="w-4 h-4" @click="setStars(i)"
          :class="i <= currentIndx ? 'text-yellow-400' : 'text-gray-300', currentIndx === i ? disabledState : enabledState" />
      </div>
    </div>
  </div>
</template>
