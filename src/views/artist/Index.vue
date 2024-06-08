<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="main">
    <UserSideBar />
    <div class="h-fit bg-gradient-to-b from-indigo-600/50">
      <div class="p-6">
        <router-view></router-view>
        <div class="flex flex-row justify-between pr-6">
          <h2 class="text-4xl font-bold">Artists</h2>
          <div class="flex gap-2">
            <select v-model="filterOrder" id="filterOrder" name="filterOrder" class="block w-full pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
              <option value="" selected>Filter by Alphabetical Order</option>
              <option value="asc">A to Z</option>
            </select>
            <button @click="resetFilters" class="px-4 py-2 text-white bg-indigo-500 rounded-md">Reset</button>
          </div>
        </div>
        <div class="">
          <ul role="list" class="mx-auto mt-20 grid max-w-2xl grid-cols-2 gap-x-8 gap-y-16 text-center sm:grid-cols-3 md:grid-cols-4 lg:mx-0 lg:max-w-none lg:grid-cols-5 xl:grid-cols-6">
            <li v-for="artist in artists" :key="artist.id">
              <RouterLink :to="`/artists/${artist.id}`">
                <img class="mx-auto h-24 w-24 rounded-full object-contain" :src="artist.avatar" alt="" />
                <h3 class="mt-6 text-base font-semibold leading-7 tracking-tight text-gray-900">{{ artist.name }}</h3>
                <p class="text-sm leading-6 text-gray-600">{{ artist.bio }}</p>
              </RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="module">
import { ref, onMounted, watch } from 'vue';
import { RouterLink } from 'vue-router';
import UserSideBar from '@/components/UserSideBar.vue';

export default {
  components: {
    UserSideBar,
    RouterLink
  },
  setup() {
    const artists = ref([]);
    const filterOrder = ref("");

    const fetchArtists = () => {
      let url = 'https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/artists';
      if (filterOrder.value) {
        url += `?orderByName=${filterOrder.value === 'asc'}`;
      }

      fetch(url)
        .then(response => response.json())
        .then(data => {
          artists.value = data.body;
        });
    };

    onMounted(() => {
      fetchArtists();
    });

    watch(filterOrder, fetchArtists);

    const resetFilters = () => {
      filterOrder.value = "";
      fetchArtists();
    };

    return {
      artists,
      filterOrder,
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
