<template>
    <div class="hidden flex-col gap-5 text-slate-800 mt-12 sm:flex">
        <div class="flex flex-col w-full lg:h-[46vh] sm:h-[40vh] mb-20 h-[10vh] duration-1000
        justify-between items-center bg-[url('/img/hero.png')] bg-no-repeat bg-center sm:px-2">
            <div class="flex justify-center items-center h-full text-3xl font-bold text-white">
                Welcome, <span class="text-rose-400">guest</span> !
            </div>
            <div class="flex justify-center items-center shadow-lg h-fit px-2 py-3 rounded-lg duration-1000 w-[90%] bg-white relative top-16">
                <div class="flex items-center justify-center w-full">
                    <div class="flex flex-col border-r border-rose-400 lg:pr-3 pr-1">
                        <label for="orderLokasi"
                            class="hover:bg-rose-400 hover:text-white duration-300 cursor-pointer lg:text-lg text-sm font-semibold border border-rose-500 rounded py-2 px-3 ">
                            Lokasi
                            <input type="text" placeholder="Pilih destinasi" id="orderLokasi"
                                class="bg-inherit text-slate-500 text-sm px-2 py-1 mt-2 rounded focus:outline-none focus:ring-1 focus:ring-rose-400 focus:bg-white duration-500 w-full">
                        </label>
                    </div>
                    <div class="flex flex-col border-r border-rose-400 lg:pr-3 pr-1 lg:ml-3 ml-1">
                        <label for="orderCheckIn"
                            class="hover:bg-rose-400 hover:text-white duration-300 cursor-pointer lg:text-lg text-sm font-semibold border border-rose-500 rounded py-2 px-3 ">
                            Check In
                            <input type="text" placeholder="mm/dd/yy" id="orderCheckIn"
                                class="bg-inherit text-slate-500 text-sm px-2 py-1 mt-2 rounded focus:outline-none focus:ring-1 focus:ring-rose-400 focus:bg-white duration-500 w-full">
                        </label>
                    </div>
                    <div class="flex flex-col border-r border-rose-400 lg:pr-3 pr-1 lg:ml-3 ml-1">
                        <label for="orderCheckOut"
                            class="hover:bg-rose-400 hover:text-white duration-300 cursor-pointer lg:text-lg text-sm font-semibold border border-rose-500 rounded py-2 px-3 ">
                            Check Out
                            <input type="text" placeholder="mm/dd/yy" id="orderCheckOut"
                                class="bg-inherit text-slate-500 text-sm px-2 py-1 mt-2 rounded focus:outline-none focus:ring-1 focus:ring-rose-400 focus:bg-white duration-500 w-full">
                        </label>
                    </div>
                    <div class="flex flex-col lg:pr-3 pr-1 lg:ml-3 ml-1">
                        <label for="orderTamu"
                            class="hover:bg-rose-400 hover:text-white duration-300 cursor-pointer lg:text-lg text-sm font-semibold border border-rose-500 rounded py-2 px-3 ">
                            Tamu
                            <input type="text" placeholder="mm/dd/yy" id="orderTamu"
                                class="bg-inherit text-slate-500 text-sm px-2 py-1 mt-2 rounded focus:outline-none focus:ring-1 focus:ring-rose-400 focus:bg-white duration-500 w-full">
                        </label>
                    </div>
                    <div class="flex flex-col">
                        <button
                            class="lg:text-lg hover:bg-rose-400 hover:text-white duration-300 cursor-pointer text-sm font-semibold border border-rose-500 rounded py-2 px-4">
                            <span><img src="/svg/book.svg" alt="" class="h-5 inline"></span>
                            pesan
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            onFocus: {
                inputLokasi: true
            }
        }
    }
}
</script>