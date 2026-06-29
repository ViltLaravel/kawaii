<template>
  <Layout v-model="searchAnime" @click="showDev" @about="showAbout">
    <Content :anime="anime" :loading="isLoading" />
  </Layout>
  <Developer :show="show" @close="hideDev" />
  <About :show="aboutVisible" @close="hideAbout" />
</template>

<script setup lang="ts">
//@ts-ignore
import Layout from "@/assets/components/Layout.vue"
//@ts-ignore
import Content from "@/assets/components/Content.vue"
//@ts-ignore
import Developer from '@/assets/components/Developer.vue'
//@ts-ignore
import About from '@/assets/components/About.vue'

import axios from "axios";
import { onMounted, ref, watch } from "vue";
import { debounce } from "vue-debounce";

const show = ref(false)
const showDev = () => { show.value = true }
const hideDev = () => { show.value = false }

const aboutVisible = ref(false)
const showAbout = () => { aboutVisible.value = true }
const hideAbout = () => { aboutVisible.value = false }

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

const searchAnime = ref('')
const anime = ref<Anime[]>([])
const isLoading = ref(false)

const fetchAnime = async () => {
  isLoading.value = true
  try {
    const res = await axios.get('https://api.jikan.moe/v4/anime')
    anime.value = res.data.data
  } catch (error) {
    console.error('Error fetching anime:', error)
  } finally {
    isLoading.value = false
  }
}

const handleSearch = async (query: string) => {
  isLoading.value = true
  try {
    const res = await axios.get(`https://api.jikan.moe/v4/anime?q=${encodeURIComponent(query)}`)
    anime.value = res.data.data
  } catch (error) {
    console.error('No anime found:', error)
  } finally {
    isLoading.value = false
  }
}

const debouncedSearch = debounce(handleSearch, 400)

onMounted(() => {
  fetchAnime()
})

watch(() => searchAnime.value, (query) => {
  if (query) {
    debouncedSearch(query)
  } else {
    fetchAnime()
  }
})
</script>
