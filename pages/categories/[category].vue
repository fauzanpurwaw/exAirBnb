<script setup>
const { category } = useRoute().params;
const { data: data } = await useFetch('https://dummyjson.com/products/category/' + category)
</script>
<template>
    <NuxtLayout :name="layouts.header" :botDir="dir"/>
    <NuxtLayout :name="layouts.container">
        <div class="flex items-center gap-3 mt-10">
            <NuxtLink  to="/" class="flex items-center gap-1 hover:text-slate-800">
                <img src="/svg/home.svg" alt="" class="h-6 inline duration-500">
                home
            </NuxtLink>
            <img src="/svg/chevronn-up.svg" alt="" class="h-6 rotate-90 inline duration-500">
            <NuxtLink  to="" class="flex items-center gap-1 hover:text-slate-800">
                {{ category }}
            </NuxtLink>
        </div>
        <div class="flex flex-col gap-5 text-slate-950 mt-10">
        <!-- <div>
            <h1 class="text-xl font-bold">Discouverez dans le monde entier</h1>
            <p class="">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et logements
                compris</p>
        </div> -->
        <div class="grid lg:grid-cols-4 sm:grid-cols-3 grid-cols-1 sm:gap-8 gap-16 w-full">
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
                    <h2 class="flex justify-end w-full font-bold">$.{{ product.price }}</h2>
                </div>
            </div>
        </div>
    </div>
    </NuxtLayout>
    <Footer />
</template>

<script>
export default {
    data() {
        return {
            layouts: {
                header: "header",
                container: "container"
            },
            dir: "../categories/"
        }
    }
}
</script>

<style>
.swiper-button-next {
    @apply flex items-center justify-center text-sm text-rose-500 hover:translate-x-1 duration-300;
    display: none;
}

.swiper-button-prev {
    @apply flex items-center justify-center text-sm text-rose-500 hover:-translate-x-1 duration-300;
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
    @apply bg-rose-400;
    width: 6px;
    height: 6px;
    opacity: 0.5;
}

.swiper-pagination-bullet-active {
    opacity: 1;
}
</style>
