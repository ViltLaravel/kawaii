<template>
  <TransitionRoot as="template" :show="show">
    <Dialog class="relative z-50" @close="emit('close')">
      <TransitionChild
        as="template"
        enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100"
        leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-black/70 backdrop-blur-sm transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
        <div class="flex min-h-full items-center justify-center p-4">
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 scale-95 translate-y-4"
            enter-to="opacity-100 scale-100 translate-y-0"
            leave="ease-in duration-200"
            leave-from="opacity-100 scale-100 translate-y-0"
            leave-to="opacity-0 scale-95 translate-y-4"
          >
            <DialogPanel class="relative w-full max-w-md glass-card p-6 sm:p-8 glow">
              <button
                type="button"
                class="absolute right-4 top-4 p-1 text-gray-500 hover:text-white rounded-lg hover:bg-white/10 transition-colors"
                @click="emit('close')"
              >
                <XMarkIcon class="h-5 w-5" />
              </button>

              <div class="flex flex-col items-center text-center">
                <div class="relative mb-5">
                  <div class="absolute -inset-2 rounded-full bg-gradient-to-r from-accent to-accent-pink opacity-30 blur-lg" />
                  <img
                    class="relative h-16 w-16 drop-shadow-lg"
                    :src="Logo"
                    alt="Kawaii Logo"
                  />
                </div>

                <h3 class="text-xl font-bold gradient-text mb-1">KAWAII</h3>
                <p class="text-sm text-gray-400 mb-5">Anime Finder</p>

                <div class="space-y-4 text-left w-full">
                  <p class="text-sm text-gray-300 leading-relaxed">
                    Kawaii is a sleek anime discovery app that lets you browse and search thousands of anime titles powered by the
                    <a href="https://jikan.moe" target="_blank" rel="noopener noreferrer" class="text-accent-light hover:underline">Jikan API</a>
                    — an open-source MyAnimeList interface.
                  </p>

                  <div class="glass-card p-4 space-y-2">
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-gray-500">Version</span>
                      <span class="text-gray-300">1.0.0</span>
                    </div>
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-gray-500">API</span>
                      <span class="text-gray-300">Jikan v4 (Free)</span>
                    </div>
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-gray-500">Built with</span>
                      <span class="text-gray-300">Vue 3 + Tailwind CSS</span>
                    </div>
                  </div>

                  <p class="text-xs text-gray-500 text-center">
                    Made with love by Nicole Amoguis
                  </p>
                </div>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup lang="ts">
import { Dialog, DialogPanel, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/24/outline'
import Logo from '@/assets/img/kawaii.png'

defineProps<{ show: boolean }>()
const emit = defineEmits(['close'])
</script>
