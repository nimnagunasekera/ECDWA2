<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="main">
    <div>
      <SideBar />
    </div>
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto">
          <h1 class="text-base font-semibold leading-6 text-gray-900">Tracks</h1>
          <p class="mt-2 text-sm text-gray-700">A list of all the tracks in this system.</p>
        </div>
        <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
          <RouterLink
            to="/admin/track/create"
            class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            Add Track
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
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    File
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Genre
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Duration
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Artist
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Album
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Sort Order
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
                <tr v-for="track in tracks" :key="track.id">
                  <td
                    class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
                  >
                    {{ track.id }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ track.name }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <a :href="track.file" target="_blank" class="text-indigo-600 hover:text-indigo-900">
                      Download
                      <span class="sr-only">, {{ track.name }}</span>
                    </a>
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ track.genre }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ track.duration }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ track.artist }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ track.album }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ track.sort_order }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <span v-if="track.status">Active</span>
                    <span v-else>Inactive</span>
                  </td>
                  <td
                    class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                  >
                    <RouterLink
                      :to="`/admin/track/${track.id}`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      View
                      <span class="sr-only">, {{ track.name }}</span>
                    </RouterLink>
                    |
                    <RouterLink
                      :to="`/admin/track/${track.id}/edit`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      Edit
                      <span class="sr-only">, {{ track.name }}</span>
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

const tracks = ref([])

fetch('https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/tracks')
  .then(response => response.json())
  .then(response => {
    console.log(response);
    tracks.value = response.body;
});

// const tracks = [
//   {
//     id: 1,
//     name: 'Track 1',
//     file: 'https://example.com/track1.mp3',
//     genre: 'Pop',
//     duration: '3:45',
//     artist: 'Artist 1',
//     album: 'Album 1',
//     sort_order: 1,
//     status: true,
//   },
//   {
//     id: 2,
//     name: 'Track 2',
//     file: 'https://example.com/track2.mp3',
//     genre: 'Rock',
//     duration: '4:15',
//     artist: 'Artist 2',
//     album: 'Album 2',
//     sort_order: 2,
//     status: false,
//   },
//   {
//     id: 3,
//     name: 'Track 3',
//     file: 'https://example.com/track3.mp3',
//     genre: 'Jazz',
//     duration: '5:00',
//     artist: 'Artist 3',
//     album: 'Album 3',
//     sort_order: 3,
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
