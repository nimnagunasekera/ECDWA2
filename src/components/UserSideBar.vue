<template>
    <div class="flex grow flex-col gap-y-5 overflow-y-auto bg-indigo-600 p-6">
      <nav class="flex flex-1 flex-col">
        <a href="/" class="p-1.5 mb-4">
          <span class="sr-only">DreamStreamer</span>
          <AppLogo class="h-10 w-auto" />
        </a>
        <ul role="list" class="flex flex-1 flex-col gap-y-7">
          <li>
            <ul role="list" class="-mx-2 space-y-1">
              <li v-for="item in navigation" :key="item.name">
                <a :href="item.href" :class="[item.current ? 'bg-indigo-700 text-white' : 'text-indigo-200 hover:text-white hover:bg-indigo-700', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold']">
                  <component :is="item.icon" :class="[item.current ? 'text-white' : 'text-indigo-200 group-hover:text-white', 'h-6 w-6 shrink-0']" aria-hidden="true" />
                  {{ item.name }}
                  <span v-if="item.count" class="ml-auto w-9 min-w-max whitespace-nowrap rounded-full bg-indigo-600 px-2.5 py-0.5 text-center text-xs font-medium leading-5 text-white ring-1 ring-inset ring-indigo-500" aria-hidden="true">{{ item.count }}</span>
                </a>
              </li>
            </ul>
          </li>
          <li>
            <div class="text-xs font-semibold leading-6 text-indigo-200">Account</div>
            <ul role="list" class="-mx-2 mt-2 space-y-1">
              <li v-for="team in teams" :key="team.name">
                <a :href="team.href" :class="[team.current ? 'bg-indigo-700 text-white' : 'text-indigo-200 hover:text-white hover:bg-indigo-700', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold']">
                  <component :is="team.icon" class="flex h-6 w-6 shrink-0 items-center justify-center rounded-lg border border-indigo-400 bg-indigo-500 text-[0.625rem] font-medium text-white"/>
                  <span class="truncate">Sign Out</span>
                </a>
              </li>
            </ul>
          </li>
        </ul>
      </nav>
    </div>
  </template>
  
<script setup>
import {
CalendarIcon,
HomeIcon,
MusicalNoteIcon,
ArrowLeftOnRectangleIcon,
} from '@heroicons/vue/24/outline';

import AppLogo from '@/components/icons/AppLogo.vue'

const navigation = [
    { name: 'Home', href: '/', icon: HomeIcon, current: true },
    { name: 'Artists', href: '/artists', icon: CalendarIcon, current: false },
    { name: 'Genres', href: '/genres', icon: CalendarIcon, current: false },
    { name: 'Albums', href: '/albums', icon: CalendarIcon, current: false },
    { name: 'Tracks', href: '/tracks', icon: MusicalNoteIcon, current: false },
]
const teams = [
{ id: 1, name: 'Sign Out', href: '/login', icon: ArrowLeftOnRectangleIcon, current: false },
]

fetch
</script>