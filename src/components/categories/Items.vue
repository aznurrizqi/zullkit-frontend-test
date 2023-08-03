<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';
import ItemCard from '../ItemCard.vue';
import { useRoute } from 'vue-router';

const items = ref([])
const category = ref([])
const route = useRoute()

async function getItemsData() {
    try {
        const response = await axios.get('http://localhost:8000/api/categories?id='+ route.params.id +'&show_product=1')
        items.value = response.data.data.products
        category.value = response.data.data
    } catch(error) {
        console.log(error)
    }
} 

// const items = ref([
//     { id: 1, title: 'Mobile UI Kit', description: 'Mobile UI Kit', image: 'items-1.jpg' },
//     { id: 2, title: 'Online Doctor Consultation', description: 'Website UI Kit', image: 'items-2.jpg' },
//     { id: 3, title: 'Banking Crypto', description: 'Mobile UI Kit', image: 'items-3.jpg' },
// ])

onMounted(() => {
    getItemsData();
})

</script>


<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">{{ category.name }}</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <ItemCard v-for="item in items" 
                :key="item.id" 
                :id="item.id" 
                :title="item.name" 
                :description="item.subtitle"
                :image="item.thumbnails" />
        </div>
    </div>
</template>
