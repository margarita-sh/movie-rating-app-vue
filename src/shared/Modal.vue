<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['submit', 'cancel']);

const form = reactive({
  name: '',
  description: '',
  image: '',
  genres: ['drama', 'comedy', 'action', 'crime'],
  inTheaters: false
});

const errors = reactive({
  name: '',
  description: '',
  image: '',
  genres: ''
});

function validate() {
  let isValid = true;

  // Reset errors
  errors.name = '';
  errors.description = '';
  errors.image = '';
  errors.genres = '';

  if (!form.name.trim()) {
    errors.name = 'Name is required.';
    isValid = false;
  }

  if (!form.description.trim()) {
    errors.description = 'Description is required.';
    isValid = false;
  }

  if (!form.image.trim()) {
    errors.image = 'Image is required.';
    isValid = false;
  }

  if (!form.genres.length) {
    errors.genres = 'Genres are required.';
    isValid = false;
  }

  return isValid;
}

function handleSubmit() {
  if (validate()) {
    emit('submit', { ...form });
  }
}

</script>

<template>
  <form @submit.prevent="handleSubmit">
  <div class="relative z-10" aria-labelledby="dialog-title" role="dialog" aria-modal="true">

    <div class="fixed inset-0 bg-gray-500/75 transition-opacity" aria-hidden="true"></div>

    <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
      <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
        <div
          class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
          <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
            <div class="sm:flex sm:items-start">

              <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left w-full">
                <h3 class="text-base font-semibold text-gray-900" id="dialog-title">Add new movie</h3>
                <div class="mt-2">
                  <p>Name:</p>
                  <input v-model="form.name" placeholder="please enter name"
                    class="w-full p-1 border border-gray-300 border-solid rounded" />
                    <span v-if="errors.name" style="color:red">{{ errors.name }}</span>
                </div>

                <div class="mt-2">
                  <p>Description:</p>
                  <textarea v-model="form.description" placeholder="please enter description"
                    class="w-full p-1 border border-gray-300 border-solid rounded" />
                    <span v-if="errors.description" style="color:red">{{ errors.description }}</span>
                </div>

                <div class="mt-2">
                  <p>Image:</p>
                  <input v-model="form.image" placeholder="please enter image url"
                    class="w-full p-1 border border-gray-300 border-solid rounded" />
                    <span v-if="errors.image" style="color:red">{{ errors.image }}</span>
                </div>

                <div class="mt-2">
                  <p>Genres:</p>
                  <textarea v-model="form.genres" placeholder="please enter genre(s)"
                    class="w-full p-1 border border-gray-300 border-solid rounded" />
                    <span v-if="errors.genres" style="color:red">{{ errors.genres }}</span>
                </div>
                <div class="mt-2">
                  <input type="checkbox" id="checkbox" v-model="form.inTheaters" /> <span>In theaters</span>
                </div>

              </div>
            </div>
          </div>
          <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
            <button type="submit"
              class="inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-xs hover:bg-red-500 sm:ml-3 sm:w-auto">Create</button>
            <button type="button" @click="$emit('cancel')"
              class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-xs ring-1 ring-gray-300 ring-inset hover:bg-gray-50 sm:mt-0 sm:w-auto">Cancel</button>
          </div>
        </div>

      </div>
    </div>
  </div>
  </form>
</template>