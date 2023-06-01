<script setup>
const { data: data } = await useLazyFetch('https://dummyjson.com/products/category/skincare?limit=3')
</script>
<template>
    <div class="flex flex-col gap-5 text-slate-950 mt-16 mb-40">
        <div>
            <h1 class="text-xl font-bold">Destinations Airbnb Plus à la Une</h1>
            <p class="">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et
                logements compris</p>
        </div>
        <div class="grid lg:grid-cols-3 sm:grid-cols-2 gap-5 w-full">
            <div class="flex flex-col gap-3 rounded hover:cursor-pointer" v-for="product in data.products">
                <div
                    class="flex justify-center items-center h-64 bg-no-repeat bg-cover bg-center bg-red-100 rounded duration-500 hover:scale-105 hover:brightness-[80%] hover:contrast-200">
                    <img :src="product.thumbnail" alt="" class="h-64 w-full brightness-75 rounded">
                    <span class="absolute"><img src="/img/Vector.png" alt=""></span>
                </div>
                <div class="flex items-center justify-between">
                    <h3 class="text-[14px] mt-1 font-bold text-slate-950">
                        {{ product.title }}
                    </h3>
                    <p>${{ product.price }}</p>
                </div>
                <p>{{ product.description }}</p>
            </div>
        </div>
    </div>
</template>