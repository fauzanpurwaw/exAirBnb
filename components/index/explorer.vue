<script setup>
const { data: data } = await useFetch('https://dummyjson.com/products/categories')
</script>
<template>
    <div class="flex flex-col gap-5 mt-8 text-slate-700 justify-center">
        <div class="flex justify-start gap-6 overflow-x-auto py-2">
            <NuxtLink :to="'categories/' + category"
                class="border bg-white h-20 flex items-center min-w-[380px] rounded-xl hover:shadow hover:cursor-pointer"
                v-for="category in data">
                    <img src="/img/explorer/explorer1.png" alt="" class="h-full rounded-l-xl">
                        <div class="flex mx-6 overflow-x-auto">
                            {{ category }}
                        </div>
            </NuxtLink>
        </div>
    </div>
</template>