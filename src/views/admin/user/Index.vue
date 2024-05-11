<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="main">
    <div>
      <SideBar />
    </div>
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto">
          <h1 class="text-base font-semibold leading-6 text-gray-900">Users</h1>
          <p class="mt-2 text-sm text-gray-700">A list of all the users in this system.</p>
        </div>
        <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
          <RouterLink
            to="/admin/user/create"
            class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            Add User
          </RouterLink>
        </div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
            <table class="min-w-full divide-y divide-gray-300">
              <thead>
                <tr>
                  <th
                    scope="col"
                    class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
                  >
                    ID
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Name
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Avatar
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Email
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Subscription
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Status
                  </th>
                  <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                    <span class="sr-only">Edit</span>
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200">
                <tr v-for="user in users" :key="user.id">
                  <td
                    class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
                  >
                    {{ user.id }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ user.name }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <img
                      :src="user.avatar"
                      alt="User avatar"
                      class="h-8 w-8 rounded-full bg-gray-50"
                    />
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ user.email }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ user.subscription }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <span v-if="user.status">Active</span>
                    <span v-else>Inactive</span>
                  </td>
                  <td
                    class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                  >
                    <RouterLink
                      :to="`/admin/user/${user.id}`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      View
                      <span class="sr-only">, {{ user.name }}</span>
                    </RouterLink>
                    |
                    <RouterLink
                      :to="`/admin/user/${user.id}/edit`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      Edit
                      <span class="sr-only">, {{ user.name }}</span>
                    </RouterLink>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
  <router-view />
</template>

<script setup>
import SideBar from '@/components/SideBar.vue';
import { RouterLink } from 'vue-router';
import { ref } from 'vue';

const users = ref([])

fetch('https://9j8qvapg12.execute-api.ap-southeast-1.amazonaws.com/dev/users')
  .then(response => response.json())
  .then(response => {
    console.log(response);
    users.value = response.body;
});

// const users = [
//   {
//     id: 1,
//     name: 'John Doe',
//     avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
//     email: 'johndoe@example.com',
//     password: 'password',
//     age: 25,
//     country: 'United States',
//     subscription: 'Premium',
//     phone: '123-456-7890',
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 2,
//     name: 'James Smith',
//     avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
//     email: 'james@example.com',
//     password: 'password',
//     age: 30,
//     country: 'United Kingdom',
//     subscription: 'Free',
//     phone: '123-456-7890',
//     sort_order: 1,
//     status: false
//   },
//   {
//     id: 3,
//     name: 'Jerry West',
//     avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
//     email: 'jerry@example.com',
//     password: 'password',
//     age: 35,
//     country: 'Australia',
//     subscription: 'Premium',
//     phone: '123-456-7890',
//     sort_order: 2,
//     status: true
//   }
// ]
</script>
<style>
.main {
  display: grid;
  grid-template-columns: 1fr 4fr;
  background: var(--color-background);
  color: var(--color-text);
  min-height: 100vh;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}
</style>
