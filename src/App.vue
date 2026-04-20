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
  <main v-if="pageData" class="container">
    <h1>{{ pageData.title }}</h1>
    
    <div v-for="category in pageData.categories" :key="category.name" class="category-block">
      <h2>{{ category.name }}</h2>
      <ul>
        <li v-for="link in category.links" :key="link.url">
          <a :href="link.url" target="_blank" rel="noopener noreferrer">
            {{ link.title }}
          </a>
        </li>
      </ul>
    </div>
  </main>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  font-family: sans-serif;
  color: #333;
}

h1 {
  text-align: center;
  color: #c0392b; /* アサルトリリィをイメージした赤系 */
  border-bottom: 2px solid #ecf0f1;
  padding-bottom: 0.5rem;
}

.category-block {
  margin-top: 2rem;
}

h2 {
  font-size: 1.2rem;
  color: #2c3e50;
  border-left: 4px solid #e74c3c;
  padding-left: 0.5rem;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 0.8rem 0;
}

a {
  text-decoration: none;
  color: #2980b9;
  font-weight: bold;
  transition: color 0.2s;
}

a:hover {
  color: #e74c3c;
  text-decoration: underline;
}
</style>
