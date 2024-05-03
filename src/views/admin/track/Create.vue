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
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <form v-on:submit.prevent="saveTrack">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">
                      {{ track.name }}
                    </DialogTitle>
                    <div class="mt-2">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <div class="sm:col-span-8">
                          <label
                            for="name"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            Name
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="name"
                                id="name"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="track.name"/>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="file"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            File
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="file"
                                name="file"
                                id="file"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="genre"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            Genre
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select
                                v-model="track.genre"
                                name="genre"
                                id="genre"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option
                                  v-for="genre in track.genre"
                                  :key="genre.id"
                                  :value="genre.id">
                                  {{ genre.name }}
                                </option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="duration"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            Duration
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="duration"
                                id="duration"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="track.duration"/>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="artist"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            Artist
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select
                                v-model="track.artist"
                                name="artist"
                                id="artist"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option
                                  v-for="artist in track.artist"
                                  :key="artist.id"
                                  :value="artist.id">
                                  {{ artist.name }}
                                </option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="album"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Album
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <select
                                v-model="track.album"
                                name="album"
                                id="album"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                              >
                                <option v-for="album in track.album" :key="album.id" :value="album.id">
                                  {{ album.name }}
                                </option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="sort_order"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            Sort Order
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="number"
                                name="sort_order"
                                id="sort_order"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="track.sort_order"/>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-1">
                          <label
                            for="status"
                            class="block text-sm font-medium leading-6 text-gray-900">
                            Status
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="checkbox"
                                name="status"
                                id="status"
                                class="block flex-1 border-0 bg-transparent py-2 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6 my-3"
                                v-model="track.status"/>
                            </div>
                          </div>
                        </div>
                        
                      </div>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6 flex gap-8">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    to="/admin/track"
                    ref="cancelButtonRef">
                    Back
                  </RouterLink>
                  <button
                    type="submit"
                    class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2">
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

const track = ref({
  id: null,
  name: '',
  file: '',
  genre: [
    { id: 1, name: 'Rock', image: 'https://randomuser.me/api/port', },
    { id: 2, name: 'Pop', image: 'https://randomuser.me/api/port', },
    { id: 3, name: 'Jazz', image: 'https://randomuser.me/api/port', },
    { id: 4, name: 'Blues', image: 'https://randomuser.me/api/port', },
    { id: 5, name: 'Country', image: 'https://randomuser.me/api/port', }
  ],
  duration: '',
  artist: [
    { id: 1, name: 'Costa', avatar: 'https://randomuser.me/api/port', },
    { id: 2, name: 'K Mac', avatar: 'https://randomuser.me/api/port', },
    { id: 3, name: 'Ravi Jay', avatar: 'https://randomuser.me/api/port', },
    { id: 4, name: 'Ridma', avatar: 'https://randomuser.me/api/port', },
    { id: 5, name: 'Thilina R', avatar: 'https://randomuser.me/api/port', }
  ],
  album: [
    { id: 1, name: 'Album 1', album_art: 'https://randomuser.me/api/port', },
    { id: 2, name: 'Album 2', album_art: 'https://randomuser.me/api/port', },
    { id: 3, name: 'Album 3', album_art: 'https://randomuser.me/api/port', },
    { id: 4, name: 'Album 4', album_art: 'https://randomuser.me/api/port', },
    { id: 5, name: 'Album 5', album_art: 'https://randomuser.me/api/port', }
  ],
  sort_order: 0,
  status: false,
})

const saveTrack = () => {
  console.log(track)

  // Call the API or function to create a new track here

  // route the user to the track list page
  router.push('/admin/track')
}
</script>