<script setup>
import { StarIcon } from "@heroicons/vue/24/solid";
import { ref } from 'vue';

defineProps({
    movieProps: {
        type: Object,
        required: true
    }
})

const currentIndx = ref(0);

function setStars($event){
  currentIndx.value = $event;
  isDisabled.value = currentIndx.value === $event;
}
const disabledState = 'cursor-not-allowed text-gray-300';
const enabledState = 'cursor-pointer';
</script>

<template>
    <div :id="movieProps.id" class="bg-white rounded-lg shadow-md overflow-hidden w-72 m-4">
        <img :src="movieProps.image" alt="movie poster" class="w-full h-96 object-cover"/>
        <div class="p-4">
      <h3 class="text-lg font-semibold text-gray-900 mb-2">{{ movieProps.name }}</h3>
      <div class="flex flex-wrap gap-2 mb-2">
        <span
          v-for="(genre, index) in movieProps.genres"
          :key="index"
          class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded-full"
        >
          {{ genre }}
        </span>
      </div>
      <p class="text-sm text-gray-700 mb-3">{{ movieProps.description }}</p>
      <div class="flex items-center">
        <span class="text-sm text-gray-600 mr-2">Rating: ({{ (currentIndx) > 0 ? (currentIndx) : 0 }}/5)</span>
          <StarIcon
            v-for="i in 5"
            :key="i"
            class="w-4 h-4"
            @click="setStars(i)"
            :class="i <= currentIndx ? 'text-yellow-400' : 'text-gray-300', currentIndx === i ? disabledState : enabledState"
          />
      </div>
    </div>
    </div>
</template>
