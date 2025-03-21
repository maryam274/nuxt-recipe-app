<template>
    <div class="p-6">
        <div v-if="chef" class="max-w-4xl mx-auto bg-white rounded-lg shadow-lg overflow-hidden">
            <img :src="chef.image" :alt="chef.name" class="w-full h-64 object-cover">
            <div class="p-6">
                <h1 class="text-4xl font-bold mb-4">{{ chef.name }}</h1>
                <p class="text-gray-700 mb-4">{{ chef.bio }}</p>
                <div class="flex justify-between items-center mb-4">
                    <div>
                        <span class="text-gray-700 font-bold">Specialty:</span>
                        <span class="text-gray-900">{{ chef.specialty }}</span>
                    </div>
                    <div>
                        <span class="text-gray-700 font-bold">Experience:</span>
                        <span class="text-gray-900">{{ chef.experience }} years</span>
                    </div>
                </div>
            </div>
        </div>
        <div v-else class="text-center text-gray-500">Loading chef details...</div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const chef = ref(null);

const fetchChef = async () => {
    try {
        const response = await fetch('/chefs.json'); // Assuming chefs.json is in the static folder
        const chefs = await response.json();
        chef.value = chefs.find((c) => c.id === parseInt(route.params.id));
    } catch (error) {
        console.error('Error fetching chef details:', error);
    }
};

onMounted(() => {
    fetchChef();
});
</script>