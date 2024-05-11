<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="main">
    <div>
      <SideBar />
    </div>
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto">
          <h1 class="text-base font-semibold leading-6 text-gray-900">Genres</h1>
          <p class="mt-2 text-sm text-gray-700">A list of all the genres in this system.</p>
        </div>
        <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
          <RouterLink
            to="/admin/genre/create"
            class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            Add Genre
          </RouterLink>
        </div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
            <table class="min-w-full divide-y divide-gray-300">
              <thead>
                <tr>
                  <th
                    scope="col"
                    class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
                  >
                    ID
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Name
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900 w-1/2">
                    Description
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Image
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Status
                  </th>
                  <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                    <span class="sr-only">Edit</span>
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200">
                <tr v-for="genre in genres" :key="genre.id">
                  <td
                    class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
                  >
                    {{ genre.id }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ genre.name }}
                  </td>
                  <td class="px-3 py-4 text-sm text-gray-500 line-clamp-2 overflow-hidden max-h-14">
                    {{ genre.description }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <img
                      :src="genre.image"
                      alt="Genre image"
                      class="h-8 w-8 rounded-full bg-gray-50"
                    />
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <span v-if="genre.status">Active</span>
                    <span v-else>Inactive</span>
                  </td>
                  <td
                    class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                  >
                    <RouterLink
                      :to="`/admin/genre/${genre.id}`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      View
                      <span class="sr-only">, {{ genre.name }}</span>
                    </RouterLink>
                    |
                    <RouterLink
                      :to="`/admin/genre/${genre.id}/edit`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      Edit
                      <span class="sr-only">, {{ genre.name }}</span>
                    </RouterLink>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
  <router-view />
</template>

<script setup>
import SideBar from '@/components/SideBar.vue';
import { RouterLink } from 'vue-router';
import { ref } from 'vue';

const genres = ref([])

fetch('https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/genres')
  .then(response => response.json())
  .then(response => {
    console.log(response);
    genres.value = response.body;
});

// const genres = [
//   {
//     id: 1,
//     name: 'Rock',
//     description: 'Rock music is a broad genre of popular music that originated as "rock and roll" in the United States in the late 1940s and early 1950s, developing into a range of different styles in the mid-1960s and later, particularly in the United States and the United Kingdom.',
//     image: 'https://images.unsplash.com/photo-1498038432885-c6f3f1b912ee',
//     sort_order: 0,
//     status: true,
//   },
//   {
//     id: 2,
//     name: 'Pop',
//     description: 'Pop music is a genre of popular music that originated in its modern form during the mid-1950s in the United States and the United Kingdom.',
//     image: 'https://images.unsplash.com/photo-1548778052-311f4bc2b502',
//     sort_order: 0,
//     status: true,
//   },
//   {
//     id: 3,
//     name: 'Hip Hop',
//     description: 'Hip hop music, also known as rap music, is a genre of popular music developed in the United States by inner-city African Americans, Latino Americans, and Caribbean Americans in the Bronx borough of New York City in the 1970s.',
//     image: 'https://images.unsplash.com/photo-1598308793232-ea6ad827ab4d',
//     sort_order: 0,
//     status: true,
//   },
//   {
//     id: 4,
//     name: 'Jazz',
//     description: 'Jazz is a music genre that originated in the African-American communities of New Orleans, United States, in the late 19th and early 20th centuries, with its roots in blues and ragtime.',
//     image: 'https://images.unsplash.com/flagged/photo-1569231290150-9c6200705c5b',
//     sort_order: 0,
//     status: true,
//   },
//   {
//     id: 5,
//     name: 'Classical',
//     description: 'Classical music is art music produced or rooted in the traditions of Western culture, generally considered to have begun in Europe after the fall of the Western Roman Empire in the late 5th century and continuing to present day.',
//     image: 'https://images.unsplash.com/photo-1465847899084-d164df4dedc6',
//     sort_order: 0,
//     status: true,
//   },
// ]
</script>
<style>
.main {
  display: grid;
  grid-template-columns: 1fr 4fr;
  background: var(--color-background);
  color: var(--color-text);
  min-height: 100vh;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}
</style>
