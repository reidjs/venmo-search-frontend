<script setup>
import { computed } from "vue"

const props = defineProps({
  result: Object
})
const to = computed(() => {
  return props?.result?.payment?.target?.user
})
const from = computed(() => {
  return props?.result?.payment?.actor
})
const note = computed(() => {
  return props?.result?.note
})
// console.log('result', result)
</script>

<template>
  <div class="border my-2 p-2">
    <div class="flex w-full space-between items-center">
      <!-- <div>{{ result }}</div> -->
      <span v-if="from" class="flex items-center flex-1">
        <img :src="from.profile_picture_url" />
        {{ from.display_name }}
      </span>
      <span class="flex-1 justify-center flex">
      💸
      </span>
      <span v-if="to" class="flex items-center justify-end flex-1">
        {{ to.display_name }}
        <img :src="to.profile_picture_url" />
      </span>
    </div>
    <div class="mt-1">{{ note }}</div>
  </div>
  <!-- <div v-if="comments.count > 0"></div> -->
</template>

<style scoped>
.flex {
  display: flex;
}
.flex-1 {
  flex: 1;
}
.w-full {
  width: 100%;
}
.justify-end {
  justify-content: flex-end;
}
.justify-center {
  justify-content: center;
}
.space-between {
  justify-content: space-between;
}
.items-center {
  align-items: center;
}
.border {
  border: 1px solid black;
}
.mt-1 {
  margin-top: 0.5rem;
}
.my-2 {
  margin: 1rem 0;
}
.p-2 {
  padding: 1.5rem;
}

img {
  width: 64px;
  height: 64px;
  border-radius: 999999px;
}
</style>