<template>
    <div class="flex sm:justify-between sm:flex-row flex-col w-full sm:gap-32 gap-3 py-6">
            <div class="flex flex-col gap-4 w-full">
                <div class="flex justify-between w-full items-center">
                    <h1>Kualitas</h1>
                    <div class="flex items-center">
                        <div class="flex bg-slate-200 w-16 h-1 rounded-full mr-1">
                            <div class="flex bg-slate-900 w-[3.4rem] h-1 rounded-full"></div>
                        </div>
                        <span><img src="/svg/star.svg" alt="" class="h-4 inline mr-1 mb-1"></span>
                        <h1>{{ rating }}</h1>
                    </div>
                </div>
                <div class="flex justify-between w-full items-center">
                    <h1>Pengiriman</h1>
                    <div class="flex items-center">
                        <div class="flex bg-slate-200 w-16 h-1 rounded-full mr-1">
                            <div class="flex bg-slate-900 w-[3.4rem] h-1 rounded-full"></div>
                        </div>
                        <span><img src="/svg/star.svg" alt="" class="h-4 inline mr-1 mb-1"></span>
                        <h1>{{ rating }}</h1>
                    </div>
                </div>
                <div class="flex justify-between w-full items-center">
                    <h1>Respon penjual</h1>
                    <div class="flex items-center">
                        <div class="flex bg-slate-200 w-16 h-1 rounded-full mr-1">
                            <div class="flex bg-slate-900 w-[3.4rem] h-1 rounded-full"></div>
                        </div>
                        <span><img src="/svg/star.svg" alt="" class="h-4 inline mr-1 mb-1"></span>
                        <h1>{{ rating }}</h1>
                    </div>
                </div>
            </div>
            <div class="flex flex-col gap-4 w-full">
                <div class="flex justify-between w-full items-center">
                    <h1>Keakuratan</h1>
                    <div class="flex items-center">
                        <div class="flex bg-slate-200 w-16 h-1 rounded-full mr-1">
                            <div class="flex bg-slate-900 w-[3.4rem] h-1 rounded-full"></div>
                        </div>
                        <span><img src="/svg/star.svg" alt="" class="h-4 inline mr-1 mb-1"></span>
                        <h1>{{ rating }}</h1>
                    </div>
                </div>
                <div class="flex justify-between w-full items-center">
                    <h1>Harga barang</h1>
                    <div class="flex items-center">
                        <div class="flex bg-slate-200 w-16 h-1 rounded-full mr-1">
                            <div class="flex bg-slate-900 w-[3.4rem] h-1 rounded-full"></div>
                        </div>
                        <span><img src="/svg/star.svg" alt="" class="h-4 inline mr-1 mb-1"></span>
                        <h1>{{ rating }}</h1>
                    </div>
                </div>
                <div class="flex justify-between w-full items-center">
                    <h1>Kemasan barang</h1>
                    <div class="flex items-center">
                        <div class="flex bg-slate-200 w-16 h-1 rounded-full mr-1">
                            <div class="flex bg-slate-900 w-[3.4rem] h-1 rounded-full"></div>
                        </div>
                        <span><img src="/svg/star.svg" alt="" class="h-4 inline mr-1 mb-1"></span>
                        <h1>{{ rating }}</h1>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
    export default {
        props: {
            rating: {
                type: String,
                default: 0
            }
        }
    }
</script>