<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="main">
    <UserSideBar />
    <div class="h-fit bg-gradient-to-b from-indigo-600/50">
      <div class="p-6">
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
                  <img class="w-36 h-36 rounded-2xl p-3" :src="track.album.album_art" alt="Track Image" />
                  <RouterLink :to="`/tracks/${track.id}`">
                    <div class="flex flex-col gap-1">
                      <span class="font-semibold text-xl">{{ track.name }}</span>
                      <span class="text-gray-500">{{ track.artist.name }}</span>
                    </div>
                  </RouterLink>
                </div>
                <button @click="togglePlay(track)" class="flex h-10 w-10 mr-3 items-center justify-center rounded-full bg-indigo-500 text-white transition-opacity group-hover:visible">
                  <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16">
                    <path v-if="isPlaying && currentTrack.id === track.id" d="M2 2h4v12H2zm8 0h4v12h-4z" />
                    <path v-else d="M3 1.713a.7.7 0 0 1 1.05-.607l10.89 6.288a.7.7 0 0 1 0 1.212L4.05 14.894A.7.7 0 0 1 3 14.288V1.713z" />
                  </svg>
                </button>
              </div>
            </li>
          </ul>
        </div>
        <footer v-if="currentTrack" class="fixed bottom-0 left-0 right-0 flex items-center justify-between border-t border-zinc-700 bg-zinc-800 px-6 py-4">
          <div class="flex items-center gap-3">
            <img class="w-20 h-20 rounded" :src="currentTrack.album.album_art" alt="Album Art" />
            <div class="flex flex-col">
              <span class="font-normal text-lg text-white">{{ currentTrack.name }}</span>
              <span class="text-xs text-zinc-400">{{ currentTrack.artist.name }}</span>
            </div>
          </div>
          <div class="flex flex-col items-center gap-2">
            <div class="flex items-center gap-6">
              <button class="text-zinc-400" @click="prevTrack">
                <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16"><path d="M3.3 1a.7.7 0 0 1 .7.7v5.15l9.95-5.744a.7.7 0 0 1 1.05.606v12.575a.7.7 0 0 1-1.05.607L4 9.149V14.3a.7.7 0 0 1-.7.7H1.7a.7.7 0 0 1-.7-.7V1.7a.7.7 0 0 1 .7-.7h1.6z"></path></svg>
              </button>
              <button class="text-zinc-400" @click="togglePlay(currentTrack)">
                <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16">
                  <path v-if="isPlaying" d="M2 2h4v12H2zm8 0h4v12h-4z" />
                  <path v-else d="M3 1.713a.7.7 0 0 1 1.05-.607l10.89 6.288a.7.7 0 0 1 0 1.212L4.05 14.894A.7.7 0 0 1 3 14.288V1.713z" />
                </svg>
              </button>
              <button class="text-zinc-400" @click="nextTrack">
                <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16"><path d="M12.7 1a.7.7 0 0 0-.7.7v5.15L2.05 1.107A.7.7 0 0 0 1 1.712v12.575a.7.7 0 0 0 1.05.607L12 9.149V14.3a.7.7 0 0 0 .7.7h1.6a.7.7 0 0 0 .7-.7V1.7a.7.7 0 0 0-.7-.7h-1.6z"></path></svg>
              </button>
            </div>
            <div class="flex items-center gap-2">
              <span class="text-xs text-zinc-400">{{ formatTime(currentTime) }}</span>
              <input type="range" v-model="progress" @input="seek" min="0" :max="duration" step="0.1" class="w-96" />
              <span class="text-xs text-zinc-400">{{ formatTime(duration) }}</span>
            </div>
          </div>
          <div class="flex items-center gap-4">
            <a href="/albums" class="text-zinc-400">
              <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16"><path d="M11.196 8 6 5v6l5.196-3z"></path><path d="M15.002 1.75A1.75 1.75 0 0 0 13.252 0h-10.5a1.75 1.75 0 0 0-1.75 1.75v12.5c0 .966.783 1.75 1.75 1.75h10.5a1.75 1.75 0 0 0 1.75-1.75V1.75zm-1.75-.25a.25.25 0 0 1 .25.25v12.5a.25.25 0 0 1-.25.25h-10.5a.25.25 0 0 1-.25-.25V1.75a.25.25 0 0 1 .25-.25h10.5z"></path></svg>
            </a>
            <a :href="`/albums/${currentTrack.album.id}`" class="text-zinc-400">
              <svg class="w-4 h-4 text-current fill-current" viewBox="0 0 16 16"><path d="M15 15H1v-1.5h14V15zm0-4.5H1V9h14v1.5zm-14-7A2.5 2.5 0 0 1 3.5 1h9a2.5 2.5 0 0 1 2.5 2.5v1H1V3.5z"></path></svg>
            </a>
          </div>
        </footer>
      </div>
    </div>
  </div>
  <router-view/>
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
    const currentTrack = ref(null);
    const audio = ref(new Audio());
    const isPlaying = ref(false);
    const progress = ref(0);
    const duration = ref(0);
    const currentTime = ref(0);
    const filterOrder = ref("");

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

    onMounted(() => {
      fetchTracks();
    });

    watch(filterOrder, fetchTracks);

    const resetFilters = () => {
      filterOrder.value = "";
      fetchTracks();
    };

    const togglePlay = (track) => {
      if (currentTrack.value && currentTrack.value.id === track.id) {
        if (isPlaying.value) {
          audio.value.pause();
        } else {
          audio.value.play();
        }
      } else {
        if (currentTrack.value) {
          audio.value.pause();
        }
        currentTrack.value = track;
        audio.value.src = track.file;
        audio.value.play();
      }
      isPlaying.value = !isPlaying.value;
    };

    const prevTrack = () => {
      const currentIndex = tracks.value.findIndex(t => t.id === currentTrack.value.id);
      if (currentIndex > 0) {
        togglePlay(tracks.value[currentIndex - 1]);
      }
    };

    const nextTrack = () => {
      const currentIndex = tracks.value.findIndex(t => t.id === currentTrack.value.id);
      if (currentIndex < tracks.value.length - 1) {
        togglePlay(tracks.value[currentIndex + 1]);
      }
    };

    const updateProgress = () => {
      currentTime.value = audio.value.currentTime;
      duration.value = audio.value.duration;
      progress.value = (audio.value.currentTime / audio.value.duration) * 100;
    };

    const seek = (event) => {
      const seekTime = (event.target.value / 100) * audio.value.duration;
      audio.value.currentTime = seekTime;
    };

    audio.value.addEventListener('timeupdate', updateProgress);
    audio.value.addEventListener('ended', nextTrack);

    const formatTime = (time) => {
      const minutes = Math.floor(time / 60);
      const seconds = Math.floor(time % 60);
      return `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
    };

    return {
      tracks,
      currentTrack,
      audio,
      isPlaying,
      progress,
      duration,
      currentTime,
      filterOrder,
      resetFilters,
      togglePlay,
      prevTrack,
      nextTrack,
      formatTime,
      seek,
    };
  }
};
</script>

