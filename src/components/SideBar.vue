<template>
    <div class="flex grow flex-col gap-y-5 overflow-y-auto border-r border-gray-200 bg-white px-6">
      <nav class="flex flex-1 flex-col">
        <ul role="list" class="flex flex-1 flex-col gap-y-7">
          <li>
            <ul role="list" class="-mx-2 space-y-1">
              <li v-for="item in navigation" :key="item.name">
                <router-link v-if="!item.children" :to="item.href" :class="[item.current ? 'bg-gray-50' : 'hover:bg-gray-50', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold text-gray-700']">
                  <component :is="item.icon" class="h-6 w-6 shrink-0 text-gray-400" aria-hidden="true" />
                  {{ item.name }}
                </router-link>
                <Disclosure as="div" v-else v-slot="{ open }">
                  <DisclosureButton :class="[item.current ? 'bg-gray-50' : 'hover:bg-gray-50', 'flex items-center w-full text-left rounded-md p-2 gap-x-3 text-sm leading-6 font-semibold text-gray-700']">
                    <component :is="item.icon" class="h-6 w-6 shrink-0 text-gray-400" aria-hidden="true" />
                    {{ item.name }}
                    <ChevronRightIcon :class="[open ? 'rotate-90 text-gray-500' : 'text-gray-400', 'ml-auto h-5 w-5 shrink-0']" aria-hidden="true" />
                  </DisclosureButton>
                  <DisclosurePanel as="ul" class="mt-1 px-2">
                    <li v-for="subItem in item.children" :key="subItem.name">
                      <!-- 44px -->
                      <router-link :to="subItem.href" :class="[subItem.current ? 'bg-gray-50' : 'hover:bg-gray-50', 'block rounded-md py-2 pr-2 pl-9 text-sm leading-6 text-gray-700']">{{ subItem.name }}</router-link>
                    </li>
                  </DisclosurePanel>
                </Disclosure>
              </li>
            </ul>
          </li>
          <li class="-mx-6 mt-auto">
            <router-link to="#" class="flex items-center gap-x-4 px-6 py-3 text-sm font-semibold leading-6 text-gray-900 hover:bg-gray-50">
              <img class="h-8 w-8 rounded-full bg-gray-50" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="" />
              <span class="sr-only">Your profile</span>
              <span aria-hidden="true">Tom Cook</span>
            </router-link>
          </li>
        </ul>
      </nav>
    </div>
  </template>
  
  <script setup>
  import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue'
  import { ChevronRightIcon } from '@heroicons/vue/20/solid'
  import {
    CalendarIcon,
    HomeIcon,
    MusicalNoteIcon,
    UserGroupIcon,
  } from '@heroicons/vue/24/outline'
  
  const navigation = [
    { name: 'Dashboard', href: '/admin', icon: HomeIcon, current: true },
    { name: 'Artists', href: '/admin/artist', icon: CalendarIcon, current: false },
    { name: 'Genres', href: '/admin/genre', icon: CalendarIcon, current: false },
    { name: 'Albums', href: '/admin/album', icon: CalendarIcon, current: false },
    { name: 'Tracks', href: '/admin/track', icon: MusicalNoteIcon, current: false },
    { name: 'Users', href: '/admin/user', icon: UserGroupIcon, current: false },
  ]
  </script>  