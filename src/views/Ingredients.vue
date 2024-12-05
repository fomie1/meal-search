<script setup>
import { ref, onMounted, computed } from 'vue'
import useAPI from '@/composables/useAPI';

const {api} = useAPI()

const keyword = ref('')
const ingredients = ref([])

onMounted(() => {
    api.get('list.php?i=list')
        .then(({ data }) => {
        ingredients.value = data.meals
    })
})

const searchIngredients = computed(() => {
    if (!searchIngredients) return ingredients

    return ingredients.value.filter( (i) => i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase()))
})



</script>


<template>
     <div class="p-8 pb-0 text-orange-500">
        <h1 class="text-4xl font-bold mb-4"> Search Meals By Ingredients</h1>
    </div>

    <!-- {{ ingredients }} -->


      <div class="p-10">
            <input type="text" v-model="keyword" class="rounded border-2 border-gray-200 w-full bg-white mb-5" placeholder="Enter ingredient name" />

            <div class="grid grid-cols-4 gap-5">
                <router-link 
                    v-for="ingredient in searchIngredients" 
                    :key="ingredient.idIngredient" 
                    :to="{name: 'MealsByIngredients', params: {ingredient: ingredient.strIngredient}}" 
                    class="bg-white rounded p-3 mb-3 shadow block">
                        <img :src="`http://www.themealdb.com/images/ingredients/${ingredient.strIngredient}-Small.png`" />
                        <h3 class="text-2xl font-bold mb-2">{{ ingredient.strIngredient }}</h3>
                </router-link>
            </div>
      </div>
</template>