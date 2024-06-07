<template>
  <div class="main">
    <UserSideBar />
    <div class="h-fit bg-gradient-to-b from-indigo-600/50">
      <div class="p-6">
        <div class="flex flex-row justify-between">
          <h2 class="text-4xl font-bold">Albums</h2>
          <div class="flex flex-col gap-1 items-start">
            <select v-model="year" id="year" name="year" class="block w-full pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
              <option value="" selected>Default</option>
              <option value="2018">2018</option>
              <option value="2020">2020</option>
              <option value="2021">2021</option>
            </select>
            <button type="button" @click="getAlbums">
              Filter By Year
            </button>
          </div>
        </div>
        <div class="mt-4 grid grid-cols-5 gap-2">
          <div v-for="album in albums" :key="album.id" class="flex flex-col p-3 cursor-pointer gap-2 rounded-md hover:bg-black/10">
            <img :src="album.album_art" class="w-48 h-48 rounded-md" width="120" height="120" alt="Album Photo" />
            <div class="flex flex-col gap-1">
              <span class="text-lg font-semibold">{{ album.name }}</span>
              <span class="text-sm text-black">{{ album.artist.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="module">
import { onMounted, ref, watch } from 'vue';
import UserSideBar from '@/components/UserSideBar.vue';

export default {
components: {
  UserSideBar
},
setup() {
  const albums = ref([]);
  const year = ref("");

  onMounted(() => {
    getAlbums()
  })

  watch(year, getAlbums, { immediate: true });

  function getAlbums() {
    fetch('https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/albums?year=' + year.value)
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      albums.value = response.body
    })
  }

  return {
    albums,
    year,
    getAlbums
  }
}
}
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