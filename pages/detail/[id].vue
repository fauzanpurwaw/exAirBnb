<script setup>
const { id } = useRoute().params;
const { data: data } = await useFetch('https://dummyjson.com/products/' + id);
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
                    <img src="../../public/svg/upload.svg" alt="" class="h-4 inline" />
                    Bagikan
                </span>
                <span class=" underline">
                    <img src="../../public/svg/heart.svg" alt="" class="h-4 inline" />
                    Simpan
                </span>
            </div>
        </div>
        <div class="flex justify-between gap-2 items-center w-full h-[480px] mt-6">
            <div class="row-span-2 col-span-2 h-[100%] w-full">
                <img :src="data.thumbnail" alt="" class="h-full w-full rounded-l-lg">
            </div>
            <div class="flex flex-col flex-nowrap justify-between gap-2 h-full w-full">
                <div class="flex flex-nowrap justify-between gap-2 h-full max-h-[235px] w-full">
                    <div class="h-full w-full">
                        <img :src="data.images[0] !== undefined ? data.images[0] : data.thumbnail" alt=""
                            class="h-full w-full">
                    </div>
                    <div class="h-full w-full">
                        <img :src="data.images[1] !== undefined ? data.images[1] : data.thumbnail" alt=""
                            class="h-full w-full rounded-tr-lg">
                    </div>
                </div>
                <div class="flex flex-nowrap justify-between gap-2 h-full max-h-[235px] w-full">
                    <div class="h-full w-full">
                        <img :src="data.images[2] !== undefined ? data.images[2] : data.thumbnail" alt=""
                            class="h-full w-full">
                    </div>
                    <div class="h-full w-full">
                        <img :src="data.images[3] !== undefined ? data.images[3] : data.thumbnail" alt=""
                            class="h-full w-full rounded-br-lg">
                    </div>
                </div>
            </div>
        </div>
        <div class="flex gap-5 mt-14">
            <div class="flex justify-between flex-[60%]">
                <h1 class="text-2xl font-sans font-medium">
                    {{ data.category }}. Tuan rumah: Valentina
                </h1>
                <h1><img src="/svg/user.svg" alt="" class="h-10"></h1>
            </div>
            <div class="flex justify-center items-center flex-[40%]">
                <div class="flex w-full h-full justify-center items-center py-5 relative">
                    <DetailOrder
                    :price="data.price"
                    :stock="data.stock"
                    :rating="data.rating"
                    />
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