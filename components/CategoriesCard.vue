<template>
    <section class="py-12 flex flex-col items-center">
        <h2 class="text-4xl font-bold text-center mb-8">Categories</h2>
        <div class="flex overflow-x-auto space-x-8 px-4">
            <div v-for="category in categories" :key="category.id" class="flex-shrink-0 flex flex-col items-center">
                <NuxtLink :to="`/categories/${category.slug}`" class="flex flex-col items-center">
                    <img :src="category.image" :alt="category.name" class="w-30 h-30 rounded-full mb-4">
                    <h3 class="text-xl font-semibold">{{ category.name }}</h3>
                </NuxtLink>
            </div>
        </div>
    </section>
</template>
<script setup>
definePageMeta({ layout: "default" })

const categories = [
    { id: 1, name: 'Pizza', slug: 'pizza', image: '/images/category1.png' },
    { id: 2, name: 'Asian Recipes', slug: 'asian-recipes', image: '/images/category2.png' },
    { id: 3, name: 'Sandwiches', slug: 'sandwiches', image: '/images/category3.png' },
    { id: 4, name: 'Sushi', slug: 'sushi', image: '/images/category4.png' },
    { id: 5, name: 'Healthy', slug: 'healthy', image: '/images/category5.png' },
    { id: 6, name: 'Desserts', slug: 'desserts', image: '/images/category6.png' },
    { id: 7, name: 'Cakes', slug: 'cakes', image: '/images/category7.png' },
    { id: 8, name: 'Sea Food', slug: 'sea-food', image: '/images/category8.png' },
    { id: 9, name: 'Chicken', slug: 'chicken', image: '/images/category9.png' }

]
</script>