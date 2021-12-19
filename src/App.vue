<script setup>
// https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import axios from 'axios'
import { ref } from 'vue'
import Results from "./components/Results.vue"

const welcome = "Type into the text box to search venmo transactions!"
const env = import.meta.env

let results  = ref([])

const fetchSearch = async query => {
  let url = env.DEV ? env.VITE_DEV_SERVER_URL : env.VITE_PROD_SERVER_URL
  url += "?q=" + query
  axios.get(url).then(res => {
    results.value = res.data
    console.log('results', results)
  })

}
const handleChange = (e) => {
  const input = e.target.value
  fetchSearch(input)
}


</script>

<template>
  <div>
    <div>{{ welcome }}</div>
    <input @input="handleChange"/>
    <Results :results="results"/>
  </div>
</template>
