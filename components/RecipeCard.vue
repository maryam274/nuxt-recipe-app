<template>
    <div>
        <!-- Recipe Cards -->
            <div  class="rounded-3xl shadow-lg">
                <NuxtLink :to="`/recipes/${recipe.id}`" class="block">
                    <img :src="recipe.image" :alt="recipe.name" class="w-full h-48 object-cover rounded-t-2xl mb-4">
                    <div class="p-4">
                        <h2 class="text-2xl font-semibold mb-2">{{ recipe.name }}</h2>
                        <div class="flex justify-between items-center mb-2">
                            <div>
                                <span class="text-gray-700">{{ recipe.price }}</span>
                                <span class="text-red-500 line-through ml-2" v-if="recipe.offerPrice">{{ recipe.offerPrice }}</span>
                            </div>
                            <div>
                                <span class="text-gray-700">{{ recipe.time }}</span>
                            </div>
                        </div>
                        <div class="flex items-center">
                            <span class="text-yellow-500 mr-2">{{ recipe.rate }}</span>
                            <i class="fas fa-star text-yellow-500"></i>
                        </div>
                    </div>
                </NuxtLink>
            </div>
    

    
    </div>
</template>

<script setup>
    const recipes = ref([]);
    const currentPage = ref(1);
    const itemsPerPage = 12;

defineProps({
    recipe: Object
});

import { ref, onMounted, computed } from 'vue';




// Fetch recipes from recipes.json
const fetchRecipes = async () => {
    try {
        const response = await fetch('/recipes.json');
        recipes.value = await response.json();
    } catch (error) {
        console.error('Error loading recipes:', error);
    }
};

// Fetch data on component mount
onMounted(() => {
    fetchRecipes();
});

</script>