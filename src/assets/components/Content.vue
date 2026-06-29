<template>
  <div v-if="loading" class="grid grid-cols-2 gap-4 sm:gap-6 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5">
    <div v-for="i in 10" :key="i" class="glass-card overflow-hidden">
      <div class="aspect-[3/4] bg-white/[0.04] animate-shimmer shimmer-bg" />
      <div class="p-3 space-y-2">
        <div class="h-4 bg-white/[0.06] rounded-md w-3/4 animate-shimmer shimmer-bg" />
        <div class="h-3 bg-white/[0.04] rounded-md w-1/2 animate-shimmer shimmer-bg" />
      </div>
    </div>
  </div>

  <div v-else-if="!anime || anime.length === 0" class="flex flex-col items-center justify-center py-20 animate-fade-in">
    <div class="text-6xl mb-4">🔍</div>
    <h3 class="text-xl font-semibold text-gray-300 mb-2">No anime found</h3>
    <p class="text-gray-500 text-sm">Try searching with a different keyword</p>
  </div>

  <TransitionGroup
    v-else
    tag="ul"
    class="grid grid-cols-2 gap-4 sm:gap-6 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5"
    enter-active-class="transition-all duration-500 ease-out"
    enter-from-class="opacity-0 translate-y-4"
    enter-to-class="opacity-100 translate-y-0"
  >
    <li
      v-for="(animes, index) in anime"
      :key="animes.mal_id"
      class="glass-card overflow-hidden card-hover group cursor-pointer"
      :style="{ animationDelay: `${index * 50}ms` }"
    >
      <a :href="animes.url" target="_blank" rel="noopener noreferrer" class="block">
        <div class="relative aspect-[3/4] overflow-hidden">
          <img
            :src="animes.images.jpg.large_image_url || animes.images.jpg.image_url"
            :alt="animes.title_english || animes.title_japanese"
            class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-110"
            loading="lazy"
          />
          <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300" />

          <div v-if="animes.score" class="absolute top-2 right-2 flex items-center gap-1 px-2 py-1 rounded-lg bg-black/60 backdrop-blur-sm text-xs font-medium">
            <StarIcon class="h-3.5 w-3.5 text-yellow-400" />
            <span class="text-yellow-100">{{ animes.score }}</span>
          </div>

          <div v-if="animes.episodes" class="absolute bottom-2 left-2 px-2 py-1 rounded-lg bg-accent/80 backdrop-blur-sm text-xs font-medium opacity-0 group-hover:opacity-100 transition-opacity duration-300">
            {{ animes.episodes }} eps
          </div>
        </div>

        <div class="p-3">
          <h3 class="text-sm font-medium text-gray-100 truncate group-hover:text-accent-light transition-colors duration-200">
            {{ animes.title_english || animes.title_japanese }}
          </h3>
          <p v-if="animes.title_japanese && animes.title_english" class="text-xs text-gray-500 truncate mt-1">
            {{ animes.title_japanese }}
          </p>
        </div>
      </a>
    </li>
  </TransitionGroup>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'
import { StarIcon } from '@heroicons/vue/24/solid'

interface Anime {
  url: string
  mal_id: string
  images: {
    jpg: {
      type: string
      image_url: string
      large_image_url: string
    }
  }
  title_english: string
  title_japanese: string
  episodes: string
  score: number
}

defineProps({
  anime: Array as PropType<Anime[]>,
  loading: Boolean,
})
</script>
