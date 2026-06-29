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
            <DialogPanel class="relative w-full max-w-sm glass-card p-6 sm:p-8 glow">
              <button
                type="button"
                class="absolute right-4 top-4 p-1 text-gray-500 hover:text-white rounded-lg hover:bg-white/10 transition-colors"
                @click="emit('close')"
              >
                <XMarkIcon class="h-5 w-5" />
              </button>

              <div class="flex flex-col items-center text-center">
                <div class="relative mb-4">
                  <div class="absolute -inset-1 rounded-full bg-gradient-to-r from-accent to-accent-pink opacity-50 blur-md" />
                  <img
                    class="relative h-24 w-24 rounded-full object-cover ring-2 ring-white/20"
                    :src="Me"
                    alt="Developer"
                  />
                </div>

                <h3 class="text-lg font-semibold text-white">Nicole Amoguis</h3>
                <p class="text-sm text-gray-400 mb-1">23 years old</p>
                <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-accent/10 text-accent-light text-xs font-medium mb-6">
                  <span class="h-1.5 w-1.5 rounded-full bg-green-400 animate-pulse" />
                  Software Engineer
                </span>

                <div class="grid grid-cols-4 gap-3 w-full">
                  <a
                    v-for="link in socialLinks"
                    :key="link.name"
                    :href="link.url"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="flex items-center justify-center p-3 rounded-xl bg-white/[0.04] hover:bg-white/10 ring-1 ring-white/[0.06] hover:ring-accent/30 transition-all duration-200 hover:-translate-y-1"
                    :title="link.name"
                  >
                    <img :src="link.icon" :alt="link.name" class="h-5 w-5 opacity-70 hover:opacity-100 transition-opacity" />
                  </a>
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
import Github from '@/assets/img/github.png'
import Avatar from '@/assets/img/avatar.png'
import Instagram from '@/assets/img/instagram.png'
import Linkedin from '@/assets/img/linkedin.png'
import Me from '@/assets/img/me.png'

defineProps<{ show: boolean }>()
const emit = defineEmits(['close'])

const socialLinks = [
  { name: 'GitHub', url: 'https://github.com/ViltLaravel/anime-finder', icon: Github },
  { name: 'LinkedIn', url: 'https://www.linkedin.com/in/nicole-amoguis-282427284/', icon: Linkedin },
  { name: 'Instagram', url: '#', icon: Instagram },
  { name: 'Portfolio', url: 'https://my-weeybsayt.vercel.app/', icon: Avatar },
]
</script>
