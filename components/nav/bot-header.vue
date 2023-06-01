<script setup>
const { data: data } = await useFetch('https://dummyjson.com/products/categories')
</script>
<template>
    <div class="flex justify-between items-center sm:px-10 px-2 h-24 w-full sticky top-20 bg-white z-[5]">
        <div class="w-full flex justify-between items-center px-2 mx-auto font-semibold text-sm">
            <div class="flex gap-8 mr-5 overflow-x-auto" ref="scroll_container">
                <div class="flex flex-col min-w-fit justify-center items-center opacity-90 hover:opacity-100 h-14 hover:cursor-pointer hover:underline underline-offset-8 my-4"
                    v-for="category in data">
                    <NuxtLink :to="dir + category" class="flex flex-col justify-center items-center">
                        <img src="/img/headerIcon/berkemah-icon.jpg" alt="" class="h-6">
                        <span class="text-sm font-normal">{{ category.toLowerCase().split('-').join(' ') }}</span>
                    </NuxtLink>
                </div>
            </div>
            <NavFilterModal />
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            dir: {
                type: String,
                default: "categories/"
            }
        }
    }
</script>