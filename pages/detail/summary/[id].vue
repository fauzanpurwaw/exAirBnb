<script setup>
const { id } = useRoute().params;
const { qty } = useRoute().query;
const { data: data } = await useFetch('https://dummyjson.com/products/' + id);
</script>

<template>
    
</template>