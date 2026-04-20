<script setup>
import { ref, onMounted } from 'vue'
import yaml from 'js-yaml'
// ?raw をつけることで文字列として読み込む
import rawYamlData from './data/links.yaml?raw'

const pageData = ref(null)

onMounted(() => {
  // YAML文字列をJavaScriptオブジェクトに変換
  pageData.value = yaml.load(rawYamlData)
})
</script>

<template>
  <div class="min-h-screen bg-white text-neutral-800 font-sans py-12 px-6">
    <main v-if="pageData" class="max-w-2xl mx-auto flex flex-col gap-12">
      
      <header>
        <h1 class="text-3xl font-bold text-neutral-900 tracking-tight">
          {{ pageData.title }}
        </h1>
        <span class="block w-16 h-1 bg-neutral-400 mt-2 mb-4"></span>
        <h2 class="text-neutral-600 mt-2">
          {{ pageData.description }}
        </h2>
      </header>

      <section v-for="category in pageData.categories" :key="category.name">
        <h2 class="text-xl font-semibold text-neutral-800 border-b-2 border-neutral-100 pb-2 mb-4">
          {{ category.name }}
        </h2>
        
        <ul class="flex flex-col gap-2">
          <li v-for="link in category.links" :key="link.url">
            <a 
              :href="link.url" 
              target="_blank" 
              rel="noopener noreferrer" 
              class="group flex items-center justify-between p-3 -mx-3 rounded-lg bg-neutral-50 hover:bg-neutral-100 transition-colors duration-200"
            >
              <span class="text-neutral-800 font-medium group-hover:text-neutral-600 transition-colors">
                {{ link.title }}
              </span>
              
              <svg 
                class="w-4 h-4 text-neutral-500 group-hover:text-neutral-500 transition-colors" 
                fill="none" 
                stroke="currentColor" 
                viewBox="0 0 24 24" 
                xmlns="http://www.w3.org/2000/svg"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
              </svg>
            </a>
          </li>
        </ul>
      </section>

    </main>
  </div>
</template>

<style scoped>
</style>
