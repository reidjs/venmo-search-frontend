<script setup>
import Result from "./Result.vue"
const props = defineProps({
  results: Array
})
</script>

<template>
<ul>
  <li v-for="result in results" :key="result._id">
    <Result :result="result"/>
  </li>
</ul>
</template>

<style scoped>
ul {
  list-style-type: none;
  padding: 0
}
</style>