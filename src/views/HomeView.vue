<template>
  <div class="main">
    <UserSideBar />
    <div class="h-fit bg-gradient-to-b from-indigo-600/50">
      <div class="p-6">
        Hello, this is the Home Page
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