<script setup>
import MealItem from './MealItem.vue';

const { meals } = defineProps({
    meals: {
        required: true, 
        type: Array
    }
})
</script>


<template>
<div class="grid grid-cols-3 gap-5 p-8">
    <MealItem v-for="meal in meals" :key="meal.idMeal" :meal="meal"></MealItem>
</div>

<div v-if="!meals.length" class="flex justifiy-center text-gray-600">
    Meals Not Found
</div>


</template>