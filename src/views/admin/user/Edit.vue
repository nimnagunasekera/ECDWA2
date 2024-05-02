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
              <form v-on:submit.prevent="saveUser">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">
                      {{ user.name }}
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
                                v-model="user.name"
                              />
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
                                v-model="user.avatar"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="email"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Email
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="email"
                                name="email"
                                id="email"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.email"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="password"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Password
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="password"
                                name="password"
                                id="password"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.password"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="age"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Age
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="number"
                                name="age"
                                id="age"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.age"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="country"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Country
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="country"
                                id="country"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.country"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="subscription"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Subscription
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="subscription"
                                id="subscription"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.subscription"
                              />
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
                          <label
                            for="phone"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Phone
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="tel"
                                name="phone"
                                id="phone"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.phone"
                              />
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
                                v-model="user.sort_order"/>
                            </div>
                          </div>
                        </div>

                        <div class="sm:col-span-4">
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
                                v-model="user.status"/>
                            </div>
                          </div>
                        </div>

                      </div>

                      <div class="text-sm text-gray-500">
                        <ul>
                          <li>name: {{ user.name }}</li>
                          <li>avatar: {{ user.avatar }}</li>
                          <li>email: {{ user.email }}</li>
                          <li>password: {{ user.password }}</li>
                          <li>age: {{ user.age }}</li>
                          <li>country: {{ user.country }}</li>
                          <li>subscription: {{ user.subscription }}</li>
                          <li>phone: {{ user.phone }}</li>
                          <li>sort_order: {{ user.sort_order }}</li>
                          <li>status: {{ user.status }}</li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6 flex gap-8">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    to="/admin/user"
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

const user = ref({
  id: 1,
  name: 'John Doe',
  avatar: 'https://randomuser.me/api/portraits',
  email: 'johndoe@example.com',
  password: 'password',
  age: 25,
  country: 'United States',
  subscription: 'Premium',
  phone: '123-456-7890',
  sort_order: 0,
  status: true
  })

const saveUser = () => {
  console.log(user)

  // route the user to the user list page
  router.push('/admin/user')
}
</script>