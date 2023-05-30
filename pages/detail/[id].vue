<script setup>
    const { id } = useRoute().params;
    const { data: data } = await useFetch('https://dummyjson.com/products/'+id);
</script>
<template>
    <DetailHeader></DetailHeader>
    <DetailContainer>
        <div class="flex items-center">
            <img src="../../public/svg/lang.svg" alt="" class="h-8 inline">
            <h1 class="text-2xl font-semibold mx-2">{{ data.title }}</h1>
        </div>
        <div class="flex justify-between items-center mt-2 text-small">
            <div class="flex gap-2 items-center">
                <img src="../../public/svg/star.svg" alt="" class="h-4">
                <span class="-ml-1">{{ data.rating }}</span> - 
                <span class="underline">{{ data.stock }} Stok tersedia</span> - 
                <span class="underline">{{ data.brand }}</span>
            </div>
            <div class="flex gap-6 items-center text-[15px]">
                <span class="underline">
                    <img src="../../public/svg/upload.svg" alt="" class="h-4 inline"/>
                    Bagikan
                </span>
                <span class=" underline">
                    <img src="../../public/svg/heart.svg" alt="" class="h-4 inline"/>
                    Simpan
                </span>
            </div>
        </div>
        <div class="grid grid-cols-4 gap-2 h-[540px] py-6">
            <div class="row-span-2 col-span-2">
                <img :src="data.thumbnail" alt="" class="h-full w-full rounded-l-lg">
            </div>
            <div class="">
                <img :src="data.thumbnail" alt="" class="h-full w-full">
            </div>
            <div class="">
                <img :src="data.thumbnail" alt="" class="h-full w-full rounded-tr-lg">
            </div>
            <div class="">
                <img :src="data.thumbnail" alt="" class="h-full w-full">
            </div>
            <div class="">
                <img :src="data.thumbnail" alt="" class="h-full w-full rounded-br-lg">
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
    }
}
</script>