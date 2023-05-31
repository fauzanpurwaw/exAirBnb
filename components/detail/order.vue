<template>
    <div class="bg-white border border-gray-300 shadow-lg rounded-xl h-fit p-5 w-[372px] duration-1000">
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
        <div class="flex mt-5 duration-1000">
            <div class="flex flex-col w-full border border-gray-400 rounded-lg duration-1000">
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
        <div class="flex justify-center items-center text-sm text-slate-500 mt-4">
            Anda belum dikenakan biaya
        </div>
        <div class="flex flex-col gap-4 mt-4 pb-6 border-gray-300 border-b">
            <div class="flex justify-between w-full">
                <div class="text-slate-600 underline cursor-pointer" @click="togglePriceDetail()">
                    $.{{ price }} x 5 nights
                </div>
                <div>
                    $.{{ price * 5 }}
                </div>
            </div>
            <Transition>
                <div class="flex flex-col shadow-lg border rounded-lg h-fit w-[330px] absolute right-[500px] bottom-[-300px] duration-1000"
                    v-show="openPriceDetail">
                    <div class="flex fixed h-screen w-screen top-0 z-[1] left-0" @click="togglePriceDetail()"></div>
                    <div class="flex justify-end px-4 py-2 z-[2] bg-white rounded-t border shadow">
                        <button @click="togglePriceDetail()"
                            class="h-5 relative right-0 top-0 hover:scale-105 duration-300">
                            <img src="/svg/close.svg" alt="" class="h-full">
                        </button>
                    </div>
                    <div class="flex justify-center flex-col px-4 border shadow bg-white z-[2]">
                        <div class="flex justify-center text-small font-semibold mb-4 pt-4">
                            Perincian Harga Dasar
                        </div>
                        <div class="flex justify-between text-small mb-4">
                            <p>
                                24/7/2023
                            </p>
                            <p class="font-medium">
                                $.{{ price }}
                            </p>
                        </div>
                        <div class="flex justify-between text-small mb-4">
                            <p>
                                24/7/2023
                            </p>
                            <p class="font-medium">
                                $.{{ price }}
                            </p>
                        </div>
                        <div class="flex justify-between text-small mb-4">
                            <p>
                                24/7/2023
                            </p>
                            <p class="font-medium">
                                $.{{ price }}
                            </p>
                        </div>
                        <div class="flex justify-between text-small mb-4">
                            <p>
                                24/7/2023
                            </p>
                            <p class="font-medium">
                                $.{{ price }}
                            </p>
                        </div>
                        <div class="flex justify-between text-small pb-4 border-b">
                            <p>
                                24/7/2023
                            </p>
                            <p class="font-medium">
                                $.{{ price }}
                            </p>
                        </div>
                    </div>
                    <div class="flex justify-between text-small font-bold py-4 px-4 rounded-b border shadow bg-white z-[2]">
                        <p>
                            Total Harga Dasar
                        </p>
                        <p>
                            $.{{ price * 5 }}
                        </p>
                    </div>
                </div>
            </Transition>
            <div class="flex justify-between">
                <div class="text-slate-600 underline cursor-pointer" @click="toggleCleaninTax()">
                    Biaya kebersihan
                </div>
                <div>
                    $.{{ cleaningPrice }}
                </div>
            </div>
            <Transition>
                <div class="absolute bottom-[-50px] duration-1000" v-show="openCleaninTax">
                    <div class="fixed h-screen w-screen top-0 right-0 z-[1]" @click="toggleCleaninTax()"></div>
                    <div
                        class="flex items-center h-fit w-[330px] gap-4 p-2 bg-white absolute z-[2] border shadow-lg rounded-lg">
                        <button @click="toggleCleaninTax()" class="w-12 hover:scale-105 duration-300"><img
                                src="/svg/close.svg" alt="" class="h-full"></button>
                        <p class="text-sm text-slate-500 py-2">Biaya satu kali yang dikenakan tuan rumah untuk menutup biaya
                            membersihkan tempat mereka.
                        </p>
                    </div>
                </div>
            </Transition>
            <div class="flex justify-between">
                <div class="text-slate-600 underline cursor-pointer" @click="toggleAdminTax()">
                    Biaya layanan Airbnb
                </div>
                <Transition>
                    <div class="absolute bottom-[-70px] duration-1000" v-show="openAdminTax">
                        <div class="fixed h-screen w-screen top-0 right-0 z-[1]" @click="toggleAdminTax()"></div>
                        <div
                            class="flex items-center h-fit w-[332px] gap-4 p-2 bg-white absolute z-[2] border shadow-lg rounded-lg">
                            <button @click="toggleAdminTax()" class="w-12 hover:scale-105 duration-300"><img
                                    src="/svg/close.svg" alt="" class="h-full"></button>
                            <p class="text-sm text-slate-500 py-2">Ini akan membantu kami membiayai pengoperasian platform
                                dan menyediakan layanan seperti dukungan 24/7 pada perjalanan Anda.</p>
                        </div>
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
            console.log(this.openPriceDetail);
        },
        toggleCleaninTax() {
            this.openCleaninTax = !this.openCleaninTax;
            console.log(this.openCleaninTax);
        },
        toggleAdminTax() {
            this.openAdminTax = !this.openAdminTax;
            console.log(this.openAdminTax);
        }
    }
}
</script>