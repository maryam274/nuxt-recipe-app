<template>
    <div>
        <header
            class="bg-cover bg-center bg-[url('/assets/images/background.png')] h-screen flex flex-col items-center justify-center text-white">
            <h1 class="text-6xl font-bold text-center">Best food for your taste</h1>
            <p class="text-lg text-center mt-4">
                Discover delectable cuisine and unforgettable moments<br>in our welcoming, culinary haven.
            </p>
            <div class="mt-10 flex items-center w-full max-w-3xl bg-white px-8 py-2 rounded-full shadow-lg">
                <i class="fas fa-search text-gray-400 ml-4"></i>
                <input type="text" placeholder="Find your Meal.." class="flex-grow p-4 text-black outline-none" />
                <button class="bg-orange-500 text-white px-8 py-3 rounded-full ml-4">Search</button>
            </div>
        </header>

        <!-- Categories Card Component -->
        <categoriesCard />

        <!-- Top Rated Recipes Section -->
        <section class="m-10">
            <router-link to="/recipes/top-rated">
                <h2 class="text-4xl font-bold mt-10 m-4 cursor-pointer hover:text-orange-500">
                    Top Rated Recipes
                </h2>
            </router-link>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 mt-6">
                <RecipeCard v-for="recipe in topRatedRecipes" :key="recipe.id" :recipe="recipe" />
            </div>
        </section>
    </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import RecipeCard from '~/components/RecipeCard.vue';
import categoriesCard from '~/components/CategoriesCard.vue';

const recipes = ref([]);

onMounted(async () => {
    try {
        const response = await fetch('/recipes.json'); // Ensure the file is inside the public folder
        recipes.value = await response.json();
    } catch (error) {
        console.error('Error loading recipes:', error);
    }
});

// Compute the top-rated recipes
const topRatedRecipes = computed(() => {
    return recipes.value
        .slice() // Create a copy to avoid mutating the original array
        .sort((a, b) => b.rate - a.rate) // Sort by highest rating
        .slice(0, 4); // Get the top 4 recipes
});
</script>
