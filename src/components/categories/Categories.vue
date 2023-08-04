<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';
import CategoryCard from '../CategoryCard.vue'

const categories = ref([])

async function getCategoriesData() {
    try {
        const response = await axios.get('http://localhost:8000/api/categories?limit=10000')
        categories.value = response.data.data.data
    } catch (error) {
        console.log(error)
    }
}

// const categories = ref([
//     { title: 'Mobile UI Kit', count: 731, image: 'categories-1.jpg' },
//     { title: 'Fonts', count: 657, image: 'categories-2.jpg' },
//     { title: 'Icon Set', count: 83559, image: 'categories-3.jpg' },
//     { title: 'Website UI Kit', count: 4500, image: 'categories-4.jpg' },
// ])

onMounted(() => {
    getCategoriesData();
})

</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">All Categories</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <CategoryCard 
                v-for="category in categories" 
                :key="category.id" 
                :id="category.id"
                :title="category.name"
                :count="category.products_count"
                :image="category.thumbnails" />
        </div>
    </div>
</template>