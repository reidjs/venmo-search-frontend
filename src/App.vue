<script setup>
// https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import axios from 'axios'
import { ref } from 'vue'
import Results from "./components/Results.vue"

const welcome = "Type into the text box to search hundreds of thousands of venmo transactions!"
const env = import.meta.env

let results  = ref([])
let searchInput = ref("")
let loading = ref(false)
let lastSearch = ref("")

const fetchSearch = async () => {
  results.value = []
  if (searchInput.value === '') {
    return
  } 
  let url = env.DEV ? env.VITE_DEV_SERVER_URL : env.VITE_PROD_SERVER_URL
  url += "?q=" + searchInput.value
  console.log('url', url)
  const res = await axios.get(url)
  lastSearch.value = searchInput.value
  results.value = res.data
  loading.value = false
}
const search = () => {
  loading.value = true
  fetchSearch()
}


</script>

<template>
  <div>
    <div>{{ welcome }}</div>
    <input @keydown.enter="search" v-model="searchInput" />
    <button @click="search">search</button>
    <div>number of results for <strong>{{ lastSearch }}</strong>: {{ loading ? 'Loading...' : results.length }}</div>
    <Results :results="results"/>
  </div>
</template>
