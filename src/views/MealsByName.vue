<script setup>
import { onMounted, computed, ref } from 'vue';
import { useRoute } from 'vue-router'
import store from '../store'
import Meals from '../components/Meals.vue'

const route = useRoute()
const keyword = ref('')
const meals = computed(() => store.state.searchedMeals)

function searchMeals() {
    if (keyword.value) {
        store.dispatch('searchMeals', keyword.value)
    }
    else {
        store.commit("setSearchedMeals", [])
    }
}

onMounted(() => {
    keyword.value = route.params.name

    if (keyword.value) {
        searchMeals()
    }
})
</script>


<template>
    <div class="p-8 pb-0 text-orange-500">
        <h1 class="text-4xl font-bold mb-4"> Search Meals By Name</h1>
    </div>

    <div class="p-8">
        <input type="text" v-model="keyword" @change="searchMeals" class="rounded border-2 border-gray-400 w-full bg-white" placeholder="Enter Name"/>

    </div>


    <Meals :meals="meals"></Meals>
</template>