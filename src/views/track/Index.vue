<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="main">
    <UserSideBar />
    <div class="h-fit bg-gradient-to-b from-indigo-600/50">
      <div class="p-6">
        <router-view></router-view>
        <div class="flex flex-row justify-between pr-6">
          <h2 class="text-4xl font-bold">Tracks</h2>
          <div class="flex gap-2">
            <select v-model="filterOrder" id="filterOrder" name="filterOrder" class="block w-full pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
              <option value="" selected>Filter by Alphabetical Order</option>
              <option value="asc">A to Z</option>
              <option value="desc">Z to A</option>
            </select>
            <button @click="resetFilters" class="px-4 py-2 text-white bg-indigo-500 rounded-md">Reset</button>
          </div>
        </div>
        <div class="mt-10">
          <ul role="list" class="mt-4 grid grid-cols-2 gap-4">
            <li v-for="track in tracks" :key="track.id">
              <div class="group flex items-center justify-between gap-4 rounded-lg bg-black/5 overflow-hidden transition-colors cursor-pointer hover:bg-black/10">
                <div class="flex flex-row items-center gap-2">
                  <img class="w-28 h-28 rounded" :src="track.album.album_art" alt="Track Image" />
                  <RouterLink :to="`/tracks/${track.id}`">
                    <div class="flex flex-col gap-1">
                      <span class="font-semibold text-xl">{{ track.name }}</span>
                      <span class="text-gray-500">{{ track.artist.name }}</span>
                    </div>
                  </RouterLink>
                </div>
                <button @click="togglePlay(track.file)" class="flex h-10 w-10 mr-3 items-center justify-center rounded-full bg-indigo-500 text-white transition-opacity group-hover:visible">
                  <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16">
                    <path v-if="isPlaying && currentTrack === track.file" d="M2 2h4v12H2zm8 0h4v12h-4z" />
                    <path v-else d="M3 1.713a.7.7 0 0 1 1.05-.607l10.89 6.288a.7.7 0 0 1 0 1.212L4.05 14.894A.7.7 0 0 1 3 14.288V1.713z" />
                  </svg>
                </button>
              </div>
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
    const tracks = ref([]);
    const filterOrder = ref("");
    const currentTrack = ref(null);
    const audio = ref(new Audio());
    const isPlaying = ref(false);

    const fetchTracks = () => {
      let url = 'https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/tracks';
      if (filterOrder.value) {
        url += `?orderByName=${filterOrder.value === 'asc'}`;
      }

      fetch(url)
        .then(response => response.json())
        .then(data => {
          tracks.value = data.body;
        });
    };

    const play = () => {
      audio.value.play();
      isPlaying.value = true;
    };

    const pause = () => {
      audio.value.pause();
      isPlaying.value = false;
    };

    const stop = () => {
      audio.value.pause();
      audio.value.currentTime = 0;
      isPlaying.value = false;
    };

    const togglePlay = (file) => {
      if (currentTrack.value === file && isPlaying.value) {
        pause();
      } else {
        if (currentTrack.value !== file) {
          audio.value.src = file;
          currentTrack.value = file;
        }
        play();
      }
    };

    onMounted(() => {
      fetchTracks();
    });

    watch(filterOrder, fetchTracks);

    const resetFilters = () => {
      filterOrder.value = "";
      fetchTracks();
    };

    return {
      tracks,
      filterOrder,
      resetFilters,
      currentTrack,
      isPlaying,
      play,
      pause,
      stop,
      togglePlay
    };
  }
};
</script>
