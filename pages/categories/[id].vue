<template>
    <div>
        <h1 class="text-4xl font-bold mb-8">Recipes for {{ categoryName }}</h1>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8 m-5 p-4">
            <div v-for="recipe in filteredRecipes" :key="recipe.id" class="rounded-lg shadow-lg bg-white">
                <img :src="recipe.image" :alt="recipe.name" class="w-full h-48 object-cover rounded-t-lg mb-4">
                <h2 class="text-2xl font-semibold m-2 text-gray-800">{{ recipe.name }}</h2>
                <div class="flex justify-between items-center m-2 p-4">
                    <div>
                        <span class="text-gray-700 font-medium">{{ recipe.price }}</span>
                        <span class="text-red-500 line-through ml-2">{{ recipe.offerPrice }}</span>
                    </div>
                    <div>
                        <span class="text-gray-600 text-sm">{{ recipe.time }}</span>
                    </div>
                </div>
                <div class="flex items-center m-2">
                    <span class="text-yellow-500 font-bold mr-1">{{ recipe.rate }}</span>
                    <i class="fas fa-star text-yellow-500"></i>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const categoryName = route.params.id

const recipes = ref([
    // 🍕 Pizza
    { id: 1, name: 'Margherita Pizza', category: 'pizza', image: '/images/margherita.jpg', price: '$12', offerPrice: '$10', time: '30 mins', rate: '4.8' },
    { id: 2, name: 'Pepperoni Pizza', category: 'pizza', image: '/images/pepperoni.jpg', price: '$15', offerPrice: '$13', time: '35 mins', rate: '4.7' },
    { id: 3, name: 'BBQ Chicken Pizza', category: 'pizza', image: '/images/bbq-chicken.jpg', price: '$16', offerPrice: '$14', time: '40 mins', rate: '4.9' },
    { id: 4, name: 'Veggie Pizza', category: 'pizza', image: '/images/veggie.jpg', price: '$14', offerPrice: '$12', time: '30 mins', rate: '4.5' },
    { id: 5, name: 'Cheese Burst Pizza', category: 'pizza', image: '/images/cheese-burst.jpg', price: '$18', offerPrice: '$15', time: '45 mins', rate: '4.6' },

    // 🍗 Chicken
    { id: 6, name: 'Chicken Curry', category: 'chicken', image: '/images/chicken-curry.jpg', price: '$15', offerPrice: '$12', time: '30 mins', rate: '4.5' },
    { id: 7, name: 'Grilled Chicken', category: 'chicken', image: '/images/grilled-chicken.jpg', price: '$17', offerPrice: '$14', time: '35 mins', rate: '4.8' },
    { id: 8, name: 'Fried Chicken', category: 'chicken', image: '/images/fried-chicken.jpg', price: '$14', offerPrice: '$12', time: '25 mins', rate: '4.7' },
    { id: 9, name: 'Chicken Tikka', category: 'chicken', image: '/images/chicken-tikka.jpg', price: '$16', offerPrice: '$13', time: '30 mins', rate: '4.6' },
    { id: 10, name: 'Butter Chicken', category: 'chicken', image: '/images/butter-chicken.jpg', price: '$18', offerPrice: '$15', time: '40 mins', rate: '4.9' },

    // 🍜 Asian Recipes
    { id: 11, name: 'Sweet & Sour Chicken', category: 'asian-recipes', image: '/images/sweet-sour.jpg', price: '$14', offerPrice: '$12', time: '25 mins', rate: '4.6' },
    { id: 12, name: 'Teriyaki Chicken', category: 'asian-recipes', image: '/images/teriyaki.jpg', price: '$16', offerPrice: '$14', time: '30 mins', rate: '4.8' },
    { id: 13, name: 'Kung Pao Shrimp', category: 'asian-recipes', image: '/images/kung-pao.jpg', price: '$17', offerPrice: '$15', time: '35 mins', rate: '4.7' },
    { id: 14, name: 'Pad Thai', category: 'asian-recipes', image: '/images/pad-thai.jpg', price: '$15', offerPrice: '$13', time: '30 mins', rate: '4.8' },
    { id: 15, name: 'Beef Bulgogi', category: 'asian-recipes', image: '/images/bulgogi.jpg', price: '$18', offerPrice: '$16', time: '40 mins', rate: '4.9' },

    // 🥪 Sandwiches
    { id: 16, name: 'Club Sandwich', category: 'sandwiches', image: '/images/club.jpg', price: '$10', offerPrice: '$8', time: '15 mins', rate: '4.7' },
    { id: 17, name: 'Philly Cheesesteak', category: 'sandwiches', image: '/images/philly.jpg', price: '$12', offerPrice: '$10', time: '20 mins', rate: '4.8' },
    { id: 18, name: 'Grilled Cheese', category: 'sandwiches', image: '/images/grilled-cheese.jpg', price: '$8', offerPrice: '$6', time: '10 mins', rate: '4.6' },
    { id: 19, name: 'BLT Sandwich', category: 'sandwiches', image: '/images/blt.jpg', price: '$9', offerPrice: '$7', time: '15 mins', rate: '4.7' },
    { id: 20, name: 'Chicken Panini', category: 'sandwiches', image: '/images/panini.jpg', price: '$11', offerPrice: '$9', time: '20 mins', rate: '4.8' },

    // 🍣 Sushi
    { id: 21, name: 'California Roll', category: 'sushi', image: '/images/california-roll.jpg', price: '$14', offerPrice: '$12', time: '25 mins', rate: '4.9' },
    { id: 22, name: 'Salmon Nigiri', category: 'sushi', image: '/images/salmon-nigiri.jpg', price: '$16', offerPrice: '$14', time: '20 mins', rate: '4.8' },
    { id: 23, name: 'Spicy Tuna Roll', category: 'sushi', image: '/images/tuna-roll.jpg', price: '$15', offerPrice: '$13', time: '30 mins', rate: '4.7' },
    { id: 24, name: 'Dragon Roll', category: 'sushi', image: '/images/dragon-roll.jpg', price: '$18', offerPrice: '$16', time: '35 mins', rate: '4.9' },
    { id: 25, name: 'Shrimp Tempura Roll', category: 'sushi', image: '/images/tempura-roll.jpg', price: '$17', offerPrice: '$15', time: '30 mins', rate: '4.8' },

    // 🍰 Cakes
    { id: 26, name: 'Chocolate Cake', category: 'cakes', image: '/images/chocolate-cake.jpg', price: '$8', offerPrice: '$6', time: '20 mins', rate: '4.9' },
    { id: 27, name: 'Vanilla Sponge Cake', category: 'cakes', image: '/images/vanilla-sponge.jpg', price: '$9', offerPrice: '$7', time: '25 mins', rate: '4.8' },
    { id: 28, name: 'Red Velvet Cake', category: 'cakes', image: '/images/red-velvet.jpg', price: '$10', offerPrice: '$8', time: '30 mins', rate: '4.7' },
    { id: 29, name: 'Strawberry Shortcake', category: 'cakes', image: '/images/strawberry-shortcake.jpg', price: '$11', offerPrice: '$9', time: '35 mins', rate: '4.8' },
    { id: 30, name: 'Carrot Cake', category: 'cakes', image: '/images/carrot-cake.jpg', price: '$10', offerPrice: '$8', time: '30 mins', rate: '4.9' },

    // 🍤 Seafood
    { id: 31, name: 'Grilled Salmon', category: 'sea-food', image: '/images/grilled-salmon.jpg', price: '$18', offerPrice: '$15', time: '35 mins', rate: '4.9' },
    { id: 32, name: 'Lobster Tail', category: 'sea-food', image: '/images/lobster-tail.jpg', price: '$25', offerPrice: '$22', time: '45 mins', rate: '4.8' },
    { id: 33, name: 'Garlic Shrimp', category: 'sea-food', image: '/images/garlic-shrimp.jpg', price: '$17', offerPrice: '$14', time: '30 mins', rate: '4.7' },
    { id: 34, name: 'Fish Tacos', category: 'sea-food', image: '/images/fish-tacos.jpg', price: '$14', offerPrice: '$12', time: '20 mins', rate: '4.6' },
    { id: 35, name: 'Crab Cakes', category: 'sea-food', image: '/images/crab-cakes.jpg', price: '$16', offerPrice: '$13', time: '30 mins', rate: '4.8' },

    //🍞 Healthy
    { id: 36, name: 'Quinoa Salad', category: 'healthy', image: '/images/quinoa-salad.jpg', price: '$10', offerPrice: '$8', time: '20 mins', rate: '4.7' },
    { id: 37, name: 'Avocado Toast', category: 'healthy', image: '/images/avocado-toast.jpg', price: '$8', offerPrice: '$6', time: '15 mins', rate: '4.6' },
    { id: 38, name: 'Grilled Salmon', category: 'healthy', image: '/images/grilled-salmon.jpg', price: '$18', offerPrice: '$15', time: '35 mins', rate: '4.8' },
    { id: 39, name: 'Fruit Bowl', category: 'healthy', image: '/images/fruit-bowl.jpg', price: '$12', offerPrice: '$10', time: '10 mins', rate: '4.9' },
    { id: 40, name: 'Green Smoothie', category: 'healthy', image: '/images/green-smoothie.jpg', price: '$7', offerPrice: '$5', time: '5 mins', rate: '4.7' },

    //🍩 Desserts
    { id: 41, name: 'Chocolate Cake', category: 'desserts', image: '/images/chocolate-cake.jpg', price: '$8', offerPrice: '$6', time: '20 mins', rate: '4.9' },
    { id: 42, name: 'Apple Pie', category: 'desserts', image: '/images/apple-pie.jpg', price: '$7', offerPrice: '$5', time: '25 mins', rate: '4.8' },
    { id: 43, name: 'Brownies', category: 'desserts', image: '/images/brownies.jpg', price: '$6', offerPrice: '$4', time: '15 mins', rate: '4.7' },
    { id: 44, name: 'Cheesecake', category: 'desserts', image: '/images/cheesecake.jpg', price: '$9', offerPrice: '$7', time: '30 mins', rate: '4.8' },
    { id: 45, name: 'Tiramisu', category: 'desserts', image: '/images/tiramisu.jpg', price: '$10', offerPrice: '$8', time: '35 mins', rate: '4.9' }

])

const filteredRecipes = computed(() => {
    return recipes.value.filter(recipe => recipe.category === categoryName)
})
</script>