<script setup>
import { ref } from 'vue';
import CategoryCard from '../CategoryCard.vue'

const categories = ref([
    { title: 'Mobile UI Kit', count: 731, image: 'categories-1.jpg' },
    { title: 'Fonts', count: 657, image: 'categories-2.jpg' },
    { title: 'Icon Set', count: 83559, image: 'categories-3.jpg' },
    { title: 'Website UI Kit', count: 4500, image: 'categories-4.jpg' },
])

</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">Top Categories</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <CategoryCard 
                v-for="category in categories" 
                :key="category.id" 
                :title="category.title"
                :count="category.count"
                :image="category.image" />
        </div>
    </div>
</template>