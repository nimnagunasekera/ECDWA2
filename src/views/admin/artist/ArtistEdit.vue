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
              <form v-on:submit.prevent="saveArtist">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">
                      {{ artist.name }}
                    </DialogTitle>
                    <div class="mt-2">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <div class="sm:col-span-8">
                          <label
                            for="name"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Name
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="name"
                                id="name"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="artist.name"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-8">
                          <label
                            for="bio"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Bio
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <textarea
                                name="bio"
                                id="bio"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="artist.bio"
                              ></textarea>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-8">
                          <label
                            for="avatar"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Avatar
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="avatar"
                                id="avatar"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="artist.avatar"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-8">
                          <label for="tracks" class="block text-sm font-medium leading-6 text-gray-900">
                            Tracks
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <ul>
                                <li v-for="track in artist.tracks" :key="track.id">
                                  <input type="checkbox" v-model="track.status" />
                                  {{ track.name }}
                                </li>
                              </ul>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-8">
                          <label for="albums" class="block text-sm font-medium leading-6 text-gray-900">
                            Albums
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <ul>
                                <li v-for="album in artist.albums" :key="album.id">
                                  <input type="checkbox" v-model="album.status" />
                                  {{ album.name }}
                                </li>
                              </ul>
                            </div>
                          </div>
                        </div>
                      </div>

                      <div class="text-sm text-gray-500">
                        <ul>
                          <li>name: {{ artist.name }}</li>
                          <li>bio: {{ artist.bio }}</li>
                          <li>avatar: {{ artist.avatar }}</li>
                          <li>tracks: {{ artist.tracks.name }}</li>
                          <li>albums: {{ artist.albums.name }}</li>
                          <li>sort_order: {{ artist.sort_order }}</li>
                          <li>status: {{ artist.status }}</li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6 flex gap-8">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    to="/admin/artist"
                    ref="cancelButtonRef"
                  >
                    Back
                  </RouterLink>
                  <button
                    type="submit"
                    class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                  >
                    Save
                  </button>
                </div>
              </form>
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
import { useRouter } from 'vue-router'

const open = ref(true)

const router = useRouter()

const artist = ref({
  id: 1,
  name: 'Costa',
  bio: 'Costa is a Sri Lankan singer, songwriter, and composer. He is a prominent figure in the Sri Lankan music industry and has gained popularity in the South Asian region. Costa has released several albums and singles throughout his career and has won numerous awards for his work.',
  avatar: 'IMAGE_URL',
  tracks: [
    { id: 1, name: 'Paata', duration: '3:45', sort_order: 0, status: true },
    { id: 2, name: 'Samanala Sandwaniya', duration: '4:12', sort_order: 0, status: true },
    { id: 3, name: 'Numba Thama', duration: '3:30', sort_order: 0, status: true }
  ],
  albums: [
    { id: 1, name: 'Album1', year: 2020, album_art: 'IMAGE_URL', studio: 'COSTA Songs', genre: 'RAP', sort_order: 0, status: true },
    { id: 2, name: 'Album2', year: 2018, album_art: 'IMAGE_URL', studio: 'COSTA Songs', genre: 'POP', sort_order: 0, status: true },
    { id: 3, name: 'Album3', year: 2016, album_art: 'IMAGE_URL', studio: 'COSTA Songs', genre: 'POP', sort_order: 0, status: true }
  ],
  sort_order: 0,
  status: true // Published etc.
  })

const saveArtist = () => {
  console.log(artist)

  // route the user to the artist list page
  router.push('/admin/artist')
}
</script>
