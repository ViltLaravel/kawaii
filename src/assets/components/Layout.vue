<template>
  <div class="min-h-screen font-poppins">
    <nav class="sticky top-0 z-50 glass border-b border-white/10">
      <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <div class="flex h-16 items-center justify-between">
          <div class="flex items-center gap-3">
            <img class="h-8 w-auto drop-shadow-lg" :src="Anime" alt="Kawaii" />
            <span class="text-lg font-semibold gradient-text hidden sm:block">KAWAII</span>
          </div>

          <div class="hidden sm:flex items-center gap-1">
            <button @click="emit('click')"
              class="px-4 py-2 text-sm font-medium text-gray-300 hover:text-white rounded-lg hover:bg-white/10 transition-all duration-200">
              Developer
            </button>
          </div>

          <button @click="mobileOpen = !mobileOpen"
            class="sm:hidden p-2 text-gray-400 hover:text-white rounded-lg hover:bg-white/10 transition-colors">
            <Bars3Icon v-if="!mobileOpen" class="h-6 w-6" />
            <XMarkIcon v-else class="h-6 w-6" />
          </button>
        </div>
      </div>

      <Transition
        enter-active-class="transition duration-200 ease-out"
        enter-from-class="opacity-0 -translate-y-2"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition duration-150 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-2"
      >
        <div v-if="mobileOpen" class="sm:hidden border-t border-white/10 px-4 py-3 space-y-1">
          <button @click="emit('click'); mobileOpen = false"
            class="block w-full text-left px-3 py-2 text-sm text-gray-300 hover:text-white rounded-lg hover:bg-white/10 transition-colors">
            Developer
          </button>
        </div>
      </Transition>
    </nav>

    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-8 sm:py-12">
      <header class="mb-8 sm:mb-12 animate-fade-in">
        <h1 class="text-3xl sm:text-4xl font-bold mb-2">
          Discover <span class="gradient-text">Anime</span>
        </h1>
        <p class="text-gray-400 text-sm sm:text-base">Search thousands of anime titles from MyAnimeList</p>
      </header>

      <div class="relative mb-8 sm:mb-10 max-w-xl animate-slide-up">
        <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
          <MagnifyingGlassIcon class="h-5 w-5 text-gray-500" />
        </div>
        <input
          type="text"
          v-model="model"
          placeholder="Search for an anime, e.g. 'Naruto'"
          class="w-full rounded-xl border-0 bg-white/[0.06] py-3 pl-11 pr-4 text-white placeholder:text-gray-500 ring-1 ring-inset ring-white/10 focus:ring-2 focus:ring-accent transition-all duration-200 text-sm sm:text-base outline-none"
        />
      </div>

      <main>
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { Bars3Icon, XMarkIcon, MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
import Anime from '@/assets/img/kawaii.png'

const model = defineModel({ required: true })
const emit = defineEmits(['click'])
const mobileOpen = ref(false)
</script>
