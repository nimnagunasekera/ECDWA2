<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = true">
        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="ease-in duration-200"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
        </TransitionChild>
  
        <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
          <div
            class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
          >
            <TransitionChild
              as="template"
              enter="ease-out duration-300"
              enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              enter-to="opacity-100 translate-y-0 sm:scale-100"
              leave="ease-in duration-200"
              leave-from="opacity-100 translate-y-0 sm:scale-100"
              leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            >
              <DialogPanel
                class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
              >
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">
                      {{ artist.name }}
                    </DialogTitle>
                    <div class="mt-2">
                      <div class="text-sm text-gray-500">
                        <ul>
                          <li>bio: {{ artist.bio }}</li>
                          <li>avatar: {{ artist.avatar }}</li>
                          <li>
                            tracks: 
                            <ul>
                              <li v-for="track in artist.tracks" :key="track.id">
                                {{ track.name }}
                              </li>
                            </ul>
                          </li>
                          <li>
                            albums: 
                            <ul>
                              <li v-for="album in artist.albums" :key="album.id">
                                {{ album.name }}
                              </li>
                            </ul>
                          </li>
                          <li>sort_order: {{ artist.sort_order }}</li>
                          <li>status: {{ artist.status }}</li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    to="/artists"
                    ref="cancelButtonRef"
                  >
                    Close
                  </RouterLink>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
  import { useRoute } from 'vue-router'
  
  const route = useRoute()
  const open = ref(true)
  const artist = ref({});
  
  fetch('https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/artists?id='+route.params.id)
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      artist.value = response.body[0]
  })
  
  // const artist = 
  // {
  //   id: 1,
  //   name: 'Costa',
  //   bio: 'Costa is a Sri Lankan singer, songwriter, and composer. He is a prominent figure in the Sri Lankan music industry and has gained popularity in the South Asian region. Costa has released several albums and singles throughout his career and has won numerous awards for his work.',
  //   avatar: 'IMAGE_URL',
  //   tracks: [
  //     { id: 1, name: 'Paata', duration: '3:45', sort_order: 0, status: true },
  //     { id: 2, name: 'Samanala Sandwaniya', duration: '4:12', sort_order: 0, status: true },
  //     { id: 3, name: 'Numba Thama', duration: '3:30', sort_order: 0, status: true }
  //   ],
  //   albums: [
  //     { id: 1, name: 'Album1', year: 2020, album_art: 'IMAGE_URL', studio: 'COSTA Songs', genre: 'RAP', sort_order: 0, status: true },
  //     { id: 2, name: 'Album2', year: 2018, album_art: 'IMAGE_URL', studio: 'COSTA Songs', genre: 'POP', sort_order: 0, status: true },
  //     { id: 3, name: 'Album3', year: 2016, album_art: 'IMAGE_URL', studio: 'COSTA Songs', genre: 'POP', sort_order: 0, status: true }
  //   ],
  //   sort_order: 0,
  //   status: true // Published etc.
  // }
  </script>
  