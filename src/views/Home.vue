<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import List from "../components/List.vue"
import Pagination from "../components/Pagination.vue"
import Controls from "../components/Controls.vue";

const router = useRouter()
const route = useRoute()

const elementsPerPage = ref(5)
const elementsInPagination = ref(5)
const currentPage = ref(1)
const elementsCount = ref(100)

const pageId = computed({
  get() {
    return route.query.pageId ?? ''
  },
  set(pageId) {
    router.replace({ query: { pageId } })
  }
})

const onChangePage = (newPage) => {
  currentPage.value = newPage
  pageId.value = newPage
}

const availableElements = computed(() => {
  return elementsCount.value / elementsPerPage.value
})

onMounted(() => {
  if (pageId.value && pageId.value <= availableElements.value) {
    currentPage.value = Number(pageId.value)
  }
})
</script>

<template>
  <h1>Home</h1>
  <Controls
    :elementsPerPage="elementsPerPage"
    :elementsInPagination="elementsInPagination"
    @changeElementsPerPage="elementsPerPage = $event"
    @changeElementsInPagination="elementsInPagination = $event"
    />
  <List
    :currentPage="currentPage"
    :elementsPerPage="elementsPerPage"
    :elementsCount="elementsCount"
  />
  <Pagination
    :currentPage="currentPage"
    :elementsPerPage="elementsPerPage"
    :elementsCount="elementsCount"
    :elementsInPagination="elementsInPagination"
    @changePage="onChangePage"
  />

</template>

<style scoped>

</style>