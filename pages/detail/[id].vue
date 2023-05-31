<script setup>
const { id } = useRoute().params;
const { data: data } = await useFetch('https://dummyjson.com/products/' + id);
</script>
<template>
    <DetailHeader></DetailHeader>
    <DetailContainer>
        <div class="flex items-center px-2">
            <img src="/svg/lang.svg" alt="" class="h-8 inline">
            <h1 class="text-2xl font-semibold mx-2">{{ data.title }}</h1>
        </div>
        <div class="flex justify-between items-center mt-2 text-small px-2">
            <div class="flex gap-2 items-center">
                <img src="/svg/star.svg" alt="" class="h-4">
                <span class="-ml-1">{{ data.rating }}</span> -
                <span class="underline">{{ data.stock }} Stok tersedia</span> -
                <span class="underline">{{ data.brand }}</span>
            </div>
            <div class="md:flex gap-6 items-center text-[15px] hidden">
                <span class="underline">
                    <img src="/svg/upload.svg" alt="" class="h-4 inline" />
                    Bagikan
                </span>
                <span class=" underline">
                    <img src="/svg/heart.svg" alt="" class="h-4 inline" />
                    Simpan
                </span>
            </div>
        </div>
        <DetailImage :images="data.images" :thumbnail="data.thumbnail" />
        <div class="flex gap-5 mt-14 px-2 md:flex-row flex-col">
            <div class="flex justify-between md:flex-[60%] bg-blue-200">
                <h1 class="text-2xl font-sans font-medium">
                    {{ data.category }}. Tuan rumah: Valentina
                </h1>
                <h1><img src="/svg/user.svg" alt="" class="h-10"></h1>
            </div>
            <div class="md:flex justify-center items-center flex-[40%] hidden bg-red-200">
                <div class="flex flex-col w-full h-full justify-center items-center py-5">
                    <DetailOrder :price="data.price" :stock="data.stock" :rating="data.rating" />
                    <div class="flex w-full justify-center items-center mt-4 text-slate-500 underline">
                        <NuxtLink to="" class="flex items-center gap-2 hover:cursor-pointer hover:text-slate-700">
                           <span><img src="/svg/flag.svg" alt="" class="h-4"></span> Laporkan iklan ini
                        </NuxtLink>
                    </div>
                </div>
            </div>
        </div>
    </DetailContainer>
    <DetailFooter />
</template>

<script>
export default {
    data() {
        return {
            layouts: {
                header: "header",
            },
        }
    },

}
</script>