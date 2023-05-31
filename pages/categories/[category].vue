<script setup>
const { category } = useRoute().params;
const { data: data } = await useFetch('https://dummyjson.com/products/category/' + category)
</script>
<template>
    <NuxtLayout :name="layouts.header" :botDir="dir"/>
    <NuxtLayout :name="layouts.container">
        <NuxtLink  to="/">
            <img src="/svg/chevronn-up.svg" alt="" class="h-16 -rotate-90 mt-5 inline hover:-translate-x-1 duration-500">
        </NuxtLink>
        <div class="flex flex-wrap items-center w-full justify-center gap-20 mt-5" >
            <div class="flex flex-col rounded w-64" v-for="product in data.products" :key="product.id">
                <div class="">
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
