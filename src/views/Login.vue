<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="flex min-h-screen flex-1 flex-col justify-center py-20 sm:px-6 lg:px-8 bg-gradient-to-t from-indigo-600/50">
      <div class="sm:mx-auto sm:w-full sm:max-w-md flex justify-center">
        <a href="/" class="">
          <span class="sr-only">DreamStreamer</span>
          <AppLogo class="h-10 w-auto" />
        </a>
      </div>
  
      <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-[480px]">
        <div class="bg-white px-6 py-12 shadow sm:rounded-lg sm:px-12">
          <form @submit.prevent="handleSubmit" class="space-y-6">
            <div>
              <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
              <div class="mt-2">
                <input id="email" name="email" type="email" autocomplete="email" required v-model="email" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
              </div>
            </div>
  
            <div>
              <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
              <div class="mt-2">
                <input id="password" name="password" type="password" autocomplete="current-password" required v-model="password" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
              </div>
            </div>
  
            <div>
              <button type="submit" class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Sign in</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { useRouter } from 'vue-router'
  import AppLogo from '@/components/icons/AppLogo.vue'
  
  const email = ref('')
  const password = ref('')
  const router = useRouter()
  
  const handleSubmit = () => {
    if (email.value === 'user@user.com' && password.value === 'password') {
      router.push('/')
    } else {
      alert('Invalid email or password')
    }
  }
  </script>
  