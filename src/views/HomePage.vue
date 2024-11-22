<script setup>
import { ref, onMounted } from 'vue'
import useAPI from '@/composables/useAPI'
import Meals from '@/components/Meals.vue'

const { api } = useAPI()
const meals = ref([])

onMounted(async () => {

  for (let index = 0; index < 9; index++) {
    api.get('random.php').then( ({data})=> meals.value.push(data.meals[0]))
    
  }
})

</script>

<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4"> Random Meals</h1>
  </div>
  <Meals :meals="meals"></Meals>
</template>
