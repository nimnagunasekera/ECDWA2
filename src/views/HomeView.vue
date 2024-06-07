<template>
  <div class="main">
    <UserSideBar />
    <div class="h-fit bg-gradient-to-b from-indigo-500/50">
      <div class="p-6">
        <div class="flex flex-row items-center justify-between">
          <h2 class="text-2xl font-semibold">Albums</h2>
          <span class="text-sm text-zinc-400">Albums</span>
        </div>
        <div class="mt-4 -ml-3 grid grid-cols-5 gap-2">
          <div v-for="album in albums" :key="album.id" class="flex flex-col p-3 cursor-pointer gap-2 rounded-md hover:bg-white/5">
            <img :src="album.album_art" class="w-48 h-48 rounded-md" width="120" height="120" alt="Album Photo" />
            <div class="flex flex-col gap-1">
              <span class="font-semibold">{{ album.name }}</span>
              <span class="text-sm text-zinc-400">{{ album.artist.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import UserSideBar from '@/components/UserSideBar.vue';

import { ref } from 'vue';

const albums = ref([])

fetch('https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/albums')
.then(response => response.json())
.then(response => {
console.log(response);
albums.value = response.body;
});
</script>

<style>
.main {
  display: grid;
  grid-template-columns: 1fr 4fr;
  background: var(--color-background);
  color: var(--color-text);
  min-height: 100vh;
}
</style>