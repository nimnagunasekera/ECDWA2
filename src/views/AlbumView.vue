<template>
    <div class="main">
      <UserSideBar />
      <div class="h-fit bg-gradient-to-b from-indigo-600/50">
        <div class="p-6">
          <div class="flex flex-row justify-between pr-6">
            <h2 class="text-4xl font-bold">Albums</h2>
            <div class="flex gap-2">
              <select v-model="year" id="year" name="year" class="block w-full pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
                <option value="" selected>Filter by Year</option>
                <option value="2015">2015</option>
                <option value="2017">2017</option>
                <option value="2019">2019</option>
                <option value="2021">2021</option>
              </select>
              <select v-model="genre" id="genre" name="genre" class="block w-full pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
                <option value="" selected>Filter by Genre</option>
                <option value="Pop">Pop</option>
                <option value="Alternative Rock">Alternative Rock</option>
                <option value="RnB">RnB</option>
                <option value="Hip Hop">Hip Hop</option>
                <option value="Country">Country</option>
                <option value="Indie Folk">Indie Folk</option>
              </select>
              <button @click="resetFilters" class="px-4 py-2 text-white bg-indigo-500 rounded-md">Reset</button>
            </div>
          </div>
          <div class="mt-4 -ml-3 grid grid-cols-5 gap-2">
            <div v-for="album in albums" :key="album.id" class="flex flex-col p-3 cursor-pointer gap-2 rounded-md hover:bg-black/10">
              <RouterLink :to="`/albums/${album.id}`">
              <img :src="album.album_art" class="w-48 h-48 rounded-md" width="120" height="120" alt="Album Photo" />
              <div class="flex flex-col gap-1">
                <span class="text-lg font-semibold">{{ album.name }}</span>
                <span class="text-sm text-black">{{ album.artist.name }}</span>
              </div>
            </RouterLink>

            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script type="module">
  import { onMounted, ref, watch } from 'vue';
  import { RouterLink } from 'vue-router';
  import UserSideBar from '@/components/UserSideBar.vue';
  
  export default {
    components: {
      UserSideBar,
      RouterLink
    },
    setup() {
      const albums = ref([]);
      const year = ref("");
      const genre = ref("");
  
      onMounted(() => {
        getAlbums();
      });
  
      watch([year, genre], getAlbums, { immediate: true });
  
      function getAlbums() {
        let url = 'https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/albums';
        let params = [];
        if (year.value) params.push(`year=${year.value}`);
        if (genre.value) params.push(`genre=${genre.value}`);
        if (params.length) url += '?' + params.join('&');

        fetch(url)
        .then((response) => response.json())
        .then((response) => {
            console.log(response)
            albums.value = response.body
        })
        }

    function resetFilters() {
    year.value = "";
    genre.value = "";
    getAlbums();
}
  
      return {
        albums,
        year,
        genre,
        getAlbums,
        resetFilters
      };
    }
  };
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
  