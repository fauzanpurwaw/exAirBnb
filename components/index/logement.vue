<script setup>
const { data: data } = await useFetch('https://dummyjson.com/products/category/home-decoration?limit=4');
</script>
<template>
    <div class="flex flex-col gap-5 text-slate-700 mt-16">
        <div>
            <h1 class="text-xl font-bold">Logements dans le monde entier</h1>
            <p class="">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et logements
                compris</p>
        </div>
        <div class="grid lg:grid-cols-4 sm:grid-cols-3 grid-cols-2 gap-5 w-full">
            <div class="flex flex-col gap-3 rounded" v-for="product in data.products"
                :key="product.id">
                <NuxtLink :to="'/detail/'+product.id">
                    <img :src="product.thumbnail" alt="" class="w-full saturate-150 h-64 hover:scale-105 duration-300 rounded-lg">
                </NuxtLink>
                <NuxtLink :to="'/categories/'+product.category">
                    <h3 class="text-[13px] text-gray-500 mt-1 mr-4 hover:text-rose-500 hover:scale-105 duration-300">
                        <span
                            class="p-1 text-[10px] border-2 border-rose-500 text-rose-500 rounded font-bold hover:bg-rose-500 hover:text-white hover:cursor-pointer">SUPERHOST</span>
                        {{ product.category }}
                    </h3>
                </NuxtLink>
                <NuxtLink :to="'/detail/'+product.id">
                    <h2 class="font-bold">{{ product.title }}</h2>
                </NuxtLink>
                <p class="flex justify-between">${{ product.price }}
                    <span class="text-emerald-800 font-bold">{{ product.rating }}<img src="/img/dicouvrez/Star1.png" alt=""
                            class="inline"></span>
                </p>
            </div>
    </div>
</div></template>