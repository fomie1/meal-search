<script setup>
const { meal } = defineProps({
    meal: {
        required: true,
        type: Object
    }
})
</script>


<template>
    <div class="bg-white shadow rounded-x1">
        <router-link :to="{}">
            <img :src="meal.strMealThumb" class="rounded-t-xl h-48 object-cover w-full"/>
        </router-link>
        <div class="p-3">
                <h3 class="font-bold">{{ meal.strMeal }}</h3>
                <p class="mb-4 line-clamp-3">{{ meal.strInstructions }}</p>
            </div>

    </div>
   
</template>