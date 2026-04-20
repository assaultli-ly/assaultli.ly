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
        <h2 class="text-neutral-600 mt-2 font-normal">
          {{ pageData.description }}
        </h2>
      </header>

      <section v-for="category in pageData.categories" :key="category.name">
        <h2 class="text-xl font-semibold text-neutral-800 border-b-2 border-neutral-100 pb-2 mb-4">
          {{ category.name }}
        </h2>

        <ul class="flex flex-col gap-1">
          <li v-for="link in category.links" :key="link.url">
            <a
              :href="link.url" 
              target="_blank" 
              rel="noopener noreferrer" 
              class="group flex items-center justify-between p-3 -mx-3 rounded-lg bg-neutral-50 hover:bg-neutral-100 transition-colors duration-200"
            >
              <div class="flex flex-col">
                <span class="text-neutral-800 font-normal group-hover:text-neutral-500 transition-colors">
                  {{ link.title }}
                </span>

                <p
                  v-if="link.description" 
                  class="text-sm text-neutral-600 group-hover:text-neutral-500 font-normal mt-0.5"
                >
                  {{ link.description }}
                </p>
              </div>

              <svg
                class="w-4 h-4 text-neutral-600 group-hover:text-neutral-400 transition-colors shrink-0 ml-4" 
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

      <section v-if="pageData.github" class="mt-4 p-8 bg-neutral-50 rounded-2xl border border-gray-100 text-center">
        <div class="flex justify-center mb-4 text-gray-700">
          <svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
            <path fill-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" clip-rule="evenodd" />
          </svg>
        </div>

        <h2 class="text-xl font-bold text-gray-900 mb-3">
          {{ pageData.github.title }}
        </h2>
        <p class="text-sm text-gray-600 mb-6 leading-relaxed">
          {{ pageData.github.description }}
        </p>

        <div class="flex flex-wrap justify-center gap-3">
          <a
            :href="pageData.github.repo_url + '/issues/new'"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-1.5 px-4 py-2 bg-white border border-gray-300 rounded-lg text-sm font-medium text-gray-700 hover:bg-gray-50 hover:text-blue-600 hover:border-blue-300 transition-all shadow-sm"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"></path></svg>
            Issueを立てる
          </a>
          <a
            :href="pageData.github.repo_url + '/pulls'"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-1.5 px-4 py-2 bg-gray-800 border border-transparent rounded-lg text-sm font-medium text-white hover:bg-gray-700 transition-all shadow-sm"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7v8a2 2 0 002 2h6M8 7V5a2 2 0 012-2h4.586a1 1 0 01.707.293l4.414 4.414a1 1 0 01.293.707V15a2 2 0 01-2 2h-2M8 7H6a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2v-2"></path></svg>
            Pull Request
          </a>
        </div>
      </section>

      <footer v-if="pageData.footer" class="mt-4 pt-4 border-t border-neutral-100 text-center">
        <p class="text-xs text-neutral-400 leading-relaxed mb-4">
          {{ pageData.footer.disclaimer }}
        </p>
        <div class="text-sm">
          <a
            :href="pageData.footer.contact_url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-neutral-500 hover:text-neutral-700 transition-colors inline-flex items-center gap-1"
          >
            <span>{{ pageData.footer.contact_label }}</span>
            <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
            </svg>
          </a>
        </div>
        <p class="mt-8 text-[10px] text-neutral-400 tracking-widest uppercase">
          assaultli.ly
        </p>
      </footer>

    </main>
  </div>
</template>

<style scoped>
</style>
