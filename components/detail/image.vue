<template>
    <div class="flex justify-between gap-2 items-center w-full h-[480px] mt-4 duration-1000">
            <div class="row-span-2 col-span-2 h-[100%] w-full">
                <img :src="thumbnail" alt="" class="h-full w-full md:rounded-l-lg">
            </div>
            <div class="flex flex-col flex-nowrap justify-between gap-2 h-full w-full">
                <div class="flex flex-nowrap justify-between gap-2 h-full max-h-[235px] w-full">
                    <div class="h-full w-full">
                        <img :src="images[0] !== undefined ? images[0] : thumbnail" alt=""
                            class="h-full w-full object-cover">
                    </div>
                    <div class="h-full w-full">
                        <img :src="images[1] !== undefined ? images[1] : thumbnail" alt=""
                            class="h-full w-full object-cover md:rounded-tr-lg">
                    </div>
                </div>
                <div class="flex flex-nowrap justify-between gap-2 h-full max-h-[235px] w-full">
                    <div class="h-full w-full">
                        <img :src="images[2] !== undefined ? images[2] : thumbnail" alt=""
                            class="h-full w-full object-cover">
                    </div>
                    <div class="h-full w-full">
                        <img :src="images[3] !== undefined ? images[3] : thumbnail" alt=""
                            class="h-full w-full object-cover md:rounded-br-lg">
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
    export default {
        props: {
            images: Array,
            thumbnail: String
        }
    }
</script>