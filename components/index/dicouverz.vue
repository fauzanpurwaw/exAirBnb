<script setup>
const { pending, data: data } = await useLazyFetch('https://dummyjson.com/products?limit=24&skip=5');
</script>
<template>
    <div class="flex flex-col gap-5 text-slate-950 mt-8 mb-16">
        <!-- <div>
            <h1 class="text-xl font-bold">Discouverez dans le monde entier</h1>
            <p class="">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et logements
                compris</p>
        </div> -->
        <div class="fixed flex justify-center items-center bg-white h-screen w-screen top-0 right-0" v-if="pending">
            <div>
                <span class=""><img src="/svg/airbnb-1.svg" alt="" class="h-40 animate-bounce"></span>
            </div>
        </div>
        <div class="grid lg:grid-cols-4 sm:grid-cols-3 grid-cols-2 gap-8 w-full" v-else>
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
                            <img :src="image" alt="" class="w-full h-56 object-cover aspect-square duration-1000 rounded-lg">
                        </NuxtLink>
                    </SwiperSlide>
                    </Swiper>
                    <NuxtLink :to="'/categories/' + product.category">
                        <h3 class="text-[10px] text-gray-500 font-bold mt-2 hover:text-rose-500 duration-300">{{ product.category }}</h3>
                    </NuxtLink>
                    <div class="flex justify-between items-center">
                        <NuxtLink :to="'/detail/' + product.id">
                            <h2 class="font-bold">{{ product.brand }}</h2>
                        </NuxtLink>
                        <p class="font-bold ml-1">{{ product.rating }} <span><img
                            src="/svg/star.svg" alt="" class="h-4 mb-1 inline"></span></p>
                    </div>
                    <p class="h-fit overflow-y-scroll truncate text-slate-500">{{ product.description }}</p>
                    <h2 class="flex justify-end w-full font-bold">{{ numberFormat(product.price) }}</h2>
                </div>
            </div>
        </div>
    </div>
</template>
<style>
.swiper-button-next {
    @apply flex items-center justify-center text-sm rounded-full w-10
     text-rose-500 hover:translate-x-1 duration-300;
    display: none;
}

.swiper-button-prev {
    @apply flex items-center justify-center text-sm
     text-rose-500 hover:-translate-x-1 duration-300;
    display: none;
}

.swiper-button-disabled {
    display: none;
}


.groupSwiper:hover .swiper-button-prev {
    display: block;
}

.groupSwiper:hover .swiper-button-next {
    display: block;
}

.swiper-pagination-bullet {
    @apply bg-black;
    width: 6px;
    height: 6px;
    opacity: 0.5;
}

.swiper-pagination-bullet-active {
    opacity: 1;
}
</style>
<script>
    export default {
        methods: {
            numberFormat(price) {
            return new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'USD',
            }).format(price)
        }
        }
    }
</script>