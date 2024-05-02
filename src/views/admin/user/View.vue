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
                    {{ user.name }}
                  </DialogTitle>
                  <div class="mt-2">
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
              <div class="mt-5 sm:mt-6">
                <RouterLink
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                  to="/admin/user"
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

const open = ref(true)

const user = {
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
}
</script>
