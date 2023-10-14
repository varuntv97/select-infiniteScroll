<script setup>
import { ref } from 'vue'
import InfiniteScroll from './components/InfiniteScroll.vue'

const selectedItem = ref()
const recordsToFetch = ref(20)

// You can set the API route here, and additionally, you can define parameters.
const dataUrl = `https://random-data-api.com/api/v2/users?size=${recordsToFetch.value}`

</script>

<template>
  <h1 class="title">Vuetify Autocomplete Infinite Scroll</h1>
  <!-- Fall through attribues is enabled -->
  <InfiniteScroll v-model="selectedItem" :dataUrl="dataUrl" label="Username" item-title="username"
    :item-value="(val) => val" />
  <pre>{{ selectedItem }}</pre>
</template>

<style scoped>
.title {
  margin-bottom: 1em;
  text-align: center;
}
</style>

