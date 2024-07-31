<script setup>
import { onMounted, ref } from 'vue'
import Items from '@/components/Items.vue'

// const names = ref([
//     { 'id': 1, 'name': 'Mostafa Ali' },
//     { 'id': 2, 'name': 'Ali Mohammad' },
//     { 'id': 3, 'name': 'Mohammad Jafar' },
//     { 'id': 4, 'name': 'Jafar Taghi' },
//     { 'id': 5, 'name': 'Mohammad Mohammadi' },
// ]);
//
// onMounted(() => {
//     localStorage.setItem("Names",JSON.stringify(names.value));
// })
</script>

<template>
    <main>
        <div>
            <Items />
        </div>
    </main>
</template>
