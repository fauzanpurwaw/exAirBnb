<script setup>
    const {data: count} = await useFetch("https://dummyjson.com/products");
</script>
<template>
    <div>
        <div>
            {{ counter }}
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            products: useFetch("https://dummyjson.com/products")
        }
    }
}
</script>