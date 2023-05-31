<template>
    <div class="bg-white border border-gray-300 shadow-lg rounded-xl h-fit p-5 w-[372px] relative left-9">
        <div class="flex justify-between items-center">
            <h1 class="text-lg font-medium">$.{{ price }} <span class="font-normal text-slate-700">/night</span>
            </h1>
            <div class="flex gap-1 text-small">
                <div class="flex items-center">
                    <img src="../../public/svg/star.svg" alt="" class="h-4">
                    <span class="">{{ rating }}</span>
                </div>
                -
                <div class="flex items-center gap-1 hover:cursor-pointer">
                    {{ stock }}
                    <span class="underline">Stock</span>
                </div>
            </div>
        </div>
        <div class="flex  mt-5">
            <div class="flex flex-col w-full border border-gray-400 rounded-lg">
                <button class="flex justify-between w-full h-full hover:border-black border rounded-lg">
                    <div class="flex justify-start h-full flex-col w-full border-r border-gray-400">
                        <h1 class="text-[10px] h-full text-left font-bold ml-3 pt-3">CHECK-OUT</h1>
                        <p class="text-[12px] h-full text-left ml-3 pb-3">MM-DD-YYYY</p>
                    </div>
                    <div class="flex justify-start h-full flex-col w-full">
                        <h1 class="text-[10px] h-full text-left font-bold ml-3 pt-3">CHECK-OUT</h1>
                        <p class="text-[12px] h-full text-left ml-3 pb-3">MM-DD-YYYY</p>
                    </div>
                </button>
                <div class="flex flex-col items w-full border-t border-gray-400">
                    <button class="flex justify-between items-center w-full h-full hover:border-black border rounded-lg">
                        <div>
                            <h1 class="text-[10px] h-full text-left font-bold ml-3 pt-3">TAMU</h1>
                            <p class="text-[12px] h-full text-left ml-3 pb-3">1 tamu</p>
                        </div>
                        <div>
                            <img src="/svg/chevronn-up.svg" alt="" class="h-5 mr-3 rotate-180">
                        </div>
                    </button>
                </div>
            </div>
        </div>
        <div
            class="flex justify-center items-center rounded-lg mt-4 bg-rose-500 h-12 cursor-pointer hover:-translate-y-1 duration-300">
            <h1 class="text-white font-semibold">Pesan</h1>
        </div>
        <div class="flex justify-center items-center text-sm text-slate-500 mt-2">
            Anda belum dikenakan biaya
        </div>
        <div class="flex flex-col gap-4 mt-4 pb-6 border-gray-300 border-b">
            <div class="flex justify-between w-full">
                <div class="text-slate-600 underline cursor-pointer" @click="togglePriceDetail()">
                    $,{{ price }} x 5 nights
                </div>
                <Transition>
                    <div class="absolute h-[350px] justify-between items-center top-0 right-0 flex flex-col bg-white w-full rounded-lg border py-5 font-normal text-sm z-[1] cursor-default"
                        v-show="openPriceDetail">
                        <div class="w-full text-left">
                            <button @click="togglePriceDetail()" class="hover:scale-105 duration-300 z-[2]"><img
                                    src="/svg/close.svg" alt="" class="h-5 w-16"></button>
                        </div>
                        <h1 class="font-semibold -mt-10">Perincian harga dasar</h1>
                        <div class="flex flex-col w-full gap-4 px-6">
                            <div class="flex justify-between w-full">
                                <div>
                                    24/7/2023
                                </div>
                                <div>
                                    $.{{ price }}
                                </div>
                            </div>
                            <div class="flex justify-between w-full">
                                <div>
                                    24/7/2023
                                </div>
                                <div>
                                    $.{{ price }}
                                </div>
                            </div>
                            <div class="flex justify-between w-full">
                                <div>
                                    24/7/2023
                                </div>
                                <div>
                                    $.{{ price }}
                                </div>
                            </div>
                            <div class="flex justify-between w-full pb-6 border-b border-black">
                                <div>
                                    24/7/2023
                                </div>
                                <div>
                                    $.{{ price }}
                                </div>
                            </div>
                        </div>
                        <div class="flex justify-between w-full px-6">
                            <h1 class="font-semibold">Total Harga Dasar</h1>
                            <h1 class="font-semibold">$.{{ price * 5 }}</h1>
                        </div>
                    </div>
                </Transition>
                <div>
                    $.{{ price * 5 }}
                </div>
            </div>
            <div class="flex justify-between">
                <div class="text-slate-600 underline cursor-pointer" @click="toggleCleaninTax()">
                    Biaya kebersihan
                </div>
                <Transition>
                    <div class="absolute h-[150px] items-center top-0 right-0 flex bg-white w-fit rounded-lg border py-5 font-normal text-sm z-[1] cursor-default"
                        v-show="openCleaninTax">
                        <button @click="toggleCleaninTax()" class="hover:scale-105 duration-300 z-[2]"><img
                                src="/svg/close.svg" alt="" class="h-5 w-16"></button>
                        <p class="px-4 underline underline-offset-2">Biaya satu kali yang dikenakan tuan
                            rumah untuk menutup biaya membersihkan tempat mereka.</p>
                    </div>
                </Transition>
                <div>
                    $.{{ cleaningPrice }}
                </div>
            </div>
            <div class="flex justify-between">
                <div class="text-slate-600 underline cursor-pointer" @click="toggleAdminTax()">
                    Biaya layanan Airbnb
                </div>
                <Transition>
                    <div class="absolute h-[150px] items-center top-0 right-0 flex bg-white w-fit rounded-lg border py-5 font-normal text-sm z-[1] cursor-default"
                        v-show="openAdminTax">
                        <button @click="toggleAdminTax()" class="hover:scale-105 duration-300 z-[2]"><img
                                src="/svg/close.svg" alt="" class="h-5 w-16"></button>
                        <p class="px-4 underline underline-offset-2">Ini akan membantu kami membiayai
                            pengoperasian platform dan menyediakan layanan seperti dukungan 24/7 pada
                            perjalanan Anda. Ini sudah termasuk PPN.</p>
                    </div>
                </Transition>
                <div>
                    $.{{ adminPrice }}
                </div>
            </div>
        </div>
        <div class="flex justify-between mt-4 font-semibold">
            <div>
                Total sebelum pajak
            </div>
            ${{ (price * 5) + cleaningPrice + adminPrice }}
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            price: {
                type: Number,
                default: 0
            },
            stock: {
                type: Number,
                default: 0
            },
            rating: {
                type: Number,
                default: 0
            },
        },
        data() {
            return {
            openPriceDetail: false,
            openCleaninTax: false,
            openAdminTax: false,
            cleaningPrice: 3.4,
            adminPrice: 11.1,
            }
        },
        methods: {
        togglePriceDetail() {
            this.openPriceDetail = !this.openPriceDetail;
            if(this.openPriceDetail == true) {
                setTimeout(() => {
                    this.openPriceDetail = false
                }, 2500);
            }
            console.log(this.openPriceDetail);
        },
        toggleCleaninTax() {
            this.openCleaninTax = !this.openCleaninTax;
            if(this.openCleaninTax == true) {
                setTimeout(() => {
                    this.openCleaninTax = false
                }, 2500);
            }
            console.log(this.openCleaninTax);
        },
        toggleAdminTax() {
            this.openAdminTax = !this.openAdminTax;
            if(this.openAdminTax == true) {
                setTimeout(() => {
                    this.openAdminTax = false
                }, 2500);
            }
            console.log(this.openAdminTax);
        }
    }
    }
</script>