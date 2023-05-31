<script setup>
    const {data: data} = await useFetch('https://dummyjson.com/products/categories')
</script>
<template>
    <div class="flex flex-col gap-5 mt-16 text-slate-700">
        <h1 class="text-xl font-bold">Explorer Airbnb</h1>
        <div class="flex justify-start gap-6 overflow-x-auto py-2">
            <div class="border h-20 flex items-center min-w-[380px] rounded-xl hover:shadow hover:cursor-pointer"  v-for="category in data">
                <NuxtLink :to="'categories/'+category">
                    <img src="/img/explorer/explorer1.png" alt="" class="h-full rounded-l-xl">
                </NuxtLink>
                <NuxtLink :to="'/categories/'+category">
                    <div class="flex mx-6 overflow-x-auto">
                        {{ category }}
                        </div>
                    </NuxtLink>
            </div>
        </div>
    </div>
</template>