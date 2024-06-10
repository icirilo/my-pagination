<script setup>
import { ref } from 'vue'

const props = defineProps({
  elementsPerPage: {
    type: Number,
    default: 10
  },
  elementsInPagination: {
    type: Number,
    default: 5
  }
})

const emit = defineEmits([ 'changeElementsPerPage', 'changeElementsInPagination' ])

const elementsPerPage = ref(props.elementsPerPage)
const elementsInPagination = ref(props.elementsInPagination)

const elementsOnPageConfig = [ 5, 10, 20, 50 ]
const elementsInPaginationConfig = [ 3, 5, 7 ]

const changeQuantity = () => {
  emit('changeElementsPerPage', elementsPerPage.value)
}

const changeQuantityPagination = () => {
  emit('changeElementsInPagination', elementsInPagination.value)
}
</script>

<template>
  <div class="controls">
    <div class="controls__inner">
      <div class="controls__col">
        <select
          v-model="elementsPerPage"
          @change="changeQuantity"
        >
          <option
            v-for="element in elementsOnPageConfig"
            :key="element"
            :value="element"
          >
            {{ element }}
          </option>
        </select>
      </div>
      <div class="controls__col">
        <select
          v-model="elementsInPagination"
          @change="changeQuantityPagination"
        >
          <option
            v-for="element in elementsInPaginationConfig"
            :key="element"
            :value="element"
          >
            {{ element }}
          </option>
        </select>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>