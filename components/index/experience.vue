<script setup>
const { data: data } = await useFetch('https://dummyjson.com/products?limit=12');
</script>
<template>
    <div class="flex flex-col gap-5 text-slate-700 mt-16">
        <div>
            <h1 class="text-xl font-bold">Expériences très bien notées</h1>
            <p class="">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et logements
                compris</p>
        </div>
        <div class="grid lg:grid-cols-6 sm:grid-cols-4 grid-cols-3 gap-3 w-full">
            <div class="flex flex-col gap-1 rounded" v-for="product in data.products" :key="product.id">
                <div>
                    <Swiper 
                    class="groupSwiper"
                    :modules="[SwiperAutoplay, SwiperEffectCreative, SwiperPagination, SwiperNavigation]"
                    :slides-per-view="1" :loop="false" :effect="'creative'" :navigation="true" :hashNavigation="{
                        watchState: true,
                    }" 
                    :pagination="{ clickable: true }" :creative-effect="{
                        prev: {
                            shadow: false,
                            translate: ['-100%', 0, -1],
                        },
                        next: {
                            translate: ['100%', 0, 0],
                        },
                    }"
                    >
                    <SwiperSlide v-for="image in product.images">
                        <NuxtLink :to="'/detail/' + product.id">
                            <img :src="image" alt="" class="w-full h-56 duration-1000 rounded-lg">
                        </NuxtLink>
                    </SwiperSlide>
                    </Swiper>  

                    <NuxtLink :to="'/categories/' + product.category">
                        <h3 class="text-[10px] text-gray-500 font-bold mt-2 hover:text-rose-500 duration-300">{{
                            product.category }}</h3>
                    </NuxtLink>
                    <div class="flex justify-between">
                        <NuxtLink :to="'/detail/' + product.id">
                            <h2 class="font-bold">{{ product.brand }}</h2>
                        </NuxtLink>
                        <p class="text-emerald-800 font-bold ">{{ product.rating }} <span><img
                                    src="/img/dicouvrez/Star1.png" alt="" class=" inline"></span></p>
                    </div>
                    <p class="h-36 overflow-y-scroll">{{ product.description }}</p>
                </div>
            </div>
        </div>
    </div>
</template>