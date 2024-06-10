<script setup>
import { ref, computed, onMounted } from 'vue'

const props = defineProps({
  elementsPerPage: {
    type: Number,
    default: 10
  },
  currentPage: {
    type: Number,
    default: 1
  },
  elementsCount: {
    type: Number,
    default: 100
  }
})

const fetchedList = ref([])
const listToShow = computed(() => {
  return fetchedList.value.slice((props.currentPage - 1) * props.elementsPerPage, props.currentPage * props.elementsPerPage)
})

const fetchList = () => {
  fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())
    .then(json => {
      fetchedList.value = json.slice(0, props.elementsCount)
    })
    .catch(error => {
      console.log(error);
    })
}

onMounted(() => {
  fetchList()
})

</script>

<template>
  <div class="list">
    <div
      v-for="element in listToShow"
      :key="element"
    >
      {{ element }}
    </div>
  </div>
</template>

<style scoped>

</style>