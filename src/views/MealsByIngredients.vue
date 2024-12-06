<script setup>
import { onMounted, computed } from 'vue'
import { useRoute } from 'vue-router'
import store from '../store'
import Meals from '../components/Meals.vue'


const meals = computed(() => store.state.mealsByIngredient)

const route = useRoute()

onMounted(() => {
    store.dispatch('searchMealsByIngredient', route.params.ingredient)
})
</script>


<template>
     <div class="p-8 pb-0 text-orange-500">
        <h1 class="text-4xl font-bold mb-4"> Meals for {{ route.params.ingredient }}</h1>
    </div>


    <Meals :meals="meals"></Meals>
</template>