<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios';


const props = defineProps({
  dataUrl: String
})

const items = ref([])

const onIntersect = (val) => {
  console.log('Is Intersecting?', val)
  if (val) {
    fetchData().then((response) => {
      console.log('On Intersect Reponse', response)
      items.value = [
        ...items.value,
        ...response.data
      ]
    })
  }
}

function fetchData() {
  return axios.get(props.dataUrl)
}

onMounted(() => {
  fetchData().then((response) => {
    console.log('On Mounted Response===>', response)
    items.value = response.data
  })
})

</script>

<template>
  <v-autocomplete v-bind="$attrs" :items="items" @change="$emit('update:modelValue', $event.target.value)">
    <template #append-item>
      <div v-intersect="onIntersect">
        Loading more items ...
      </div>
    </template>
  </v-autocomplete>
</template>

<style scoped></style>
