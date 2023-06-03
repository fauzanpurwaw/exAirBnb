<script setup>
const { id } = useRoute().params;
const { data: data } = await useFetch('https://dummyjson.com/products/' + id);
</script>
<template>
    <DetailHeader></DetailHeader>
    <DetailContainer>
        <div class="flex items-center px-2">
            <img src="/svg/lang.svg" alt="" class="h-8 inline">
            <h1 class="text-xl font-semibold mx-2">{{ data.title }}</h1>
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
        <div class="flex item gap-5 mt-14 px-2 md:flex-row flex-col">
            <div class="md:flex-[60%]">
                <h1 class="flex justify-between items-center text-2xl font-sans font-medium">
                    <div>
                        {{ data.category.toUpperCase() }}
                        <h2 class="text-xl">{{ data.brand }}: {{ data.title }}</h2>
                    </div>
                    <h1><img src="/svg/user.svg" alt="" class="h-10"></h1>
                </h1>
                <p class="text-lg py-6">{{ data.description }}</p>
                <h3 class="text-lg font-semibold ">Pengiriman</h3>
                <div class="flex flex-col py-4">
                    <p>
                        <span><img src="/svg/location.svg" alt="" class="h-6 inline px-2"></span>
                        Dikirim dari <span class="font-medium">Kota Denpasar.</span>
                    </p>
                    <p>
                        <span><img src="/svg/location.svg" alt="" class="h-6 inline px-2"></span>
                        Pengemasan reguler <span class="font-medium">$3.4</span>
                    </p>
                </div>
                <div class="flex flex-col px-2 duration-1000">
                    <p class="h-64 overflow-y-hidden duration-1000" :class="{ 'h-fit': isShortDetail }">
                        Brand : Casio <br>
                        Model No : LA-20WH-8ADF <br>
                        Gender : wanita <br>
                        Garansi produk : Garansi 1 Tahun <br>
                        Case diameter : 30.4 mm<br>
                        Case thickness : 8.6 mm<br>
                        Water resistant : 30 Meters/3 ATM/3 BAR<br>
                        Case material : Plastic/Resin<br>
                        Case back : Screw case back<br>
                        Glass material : Mineral crystal<br>
                        Strap material : Rubber/Silicon/Resin/Karet<br>
                        Clasp : Buckle<br>
                        Calendar : Perpetual Calendar<br>
                        Luminious / LumiBrite : No<br>
                        Movement :Quartz Movement<br>
                        Approx. Battery Life :5 years on CR1616<br>
                        Stopwatch :1/100-second stopwatch , Measuring capacity: 59'59.99: , Measuring modes: Elapsed time,
                        split
                        time, 1st-2nd place times<br>
                        Regular timekeeping :Hour, minute, second, pm, date, day<br>
                        Features :LED light , Daily alarm , Hourly time signal , Auto-calendar (auto calendar set at 28 days
                        for
                        February) , 12/24-hour format<br>
                        Accuracy :+-30 seconds per month<br>
                        Dial Color :Digital Dial<br>
                        Weight :16g<br>
                        Weight after packing :approx. 500g<br>
                        What's Inside Box :1x Casio General LA-20WH-8ADF Ladies Digital Dial Grey Resin Strap , 1x Manual
                        Book ,
                        1x Warranty Card , 1x Box Jam Tangan<br>
                    </p>
                    <div class="flex py-3 text-rose-500 hover:cursor-pointer hover:text-rose-700" v-if="isShortDetail"
                        @click="isShortDetail = !isShortDetail">
                        Selenkapnya..
                    </div>
                    <div class="flex py-2 text-rose-500 hover:cursor-pointer hover:text-rose-700" v-else
                        @click="isShortDetail = !isShortDetail">
                        Lebih sedikit..
                    </div>
                </div>
            </div>
            <div class="flex justify-center flex-[40%]">
                <div class="flex w-full h-full justify-center py-5 lg:ml-24">
                    <div class="flex h-fit flex-col sticky top-4 ">
                        <DetailOrder :price="data.price" :stock="data.stock" :rating="data.rating" :title="data.title" :id="data.id" />
                        <div class="flex w-full justify-center items-center mt-4 text-slate-500 underline">
                            <NuxtLink to="" class="flex items-center gap-2 hover:cursor-pointer hover:text-slate-700">
                                <span><img src="/svg/flag.svg" alt="" class="h-4"></span> Laporkan produk ini
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex flex-col w-full mt-16 px-2">
            <div class="flex w-full items-center text-2xl font-medium pt-12 border-t border-slate-300">
                <span><img src="/svg/star.svg" alt="" class="h-6"></span> {{ data.rating }} Rating
            </div>
            <DetailRating :rating="data.rating" />
            <div class="grid sm:grid-cols-2 grid-cols-1 gap-12 py-8">
                <div class="flex flex-col">
                    <div class="flex items-center gap-2">
                        <span><img src="/svg/user.svg" alt="" class="h-10"></span>
                        <div>
                            <h1 class="font-medium">Indra</h1>
                            <h2 class="text-slate-600">September 2021</h2>
                        </div>
                    </div>
                    <p class="">Pengalaman menginap di veluvana sangat memuaskan, apa yang disampaikan di deskripsi dan foto sesuai.
                        Terutama View dr lantai 2 sangat bagus, sayang cuaca kurang baik sehingga...</p>
                    <div class="font-medium underline py-1">
                        <a class="cursor-pointer">
                            Tampilkan lebih banyak <span><img src="/svg/chevronn-up.svg" alt="" class="h-4 inline rotate-90"></span>
                        </a>
                    </div>
                </div>
                <div class="flex flex-col">
                    <div class="flex items-center gap-2">
                        <span><img src="/svg/user.svg" alt="" class="h-10"></span>
                        <div>
                            <h1 class="font-medium">Indra</h1>
                            <h2 class="text-slate-600">September 2021</h2>
                        </div>
                    </div>
                    <p class="">Pengalaman menginap di veluvana sangat memuaskan, apa yang disampaikan di deskripsi dan foto sesuai.
                        Terutama View dr lantai 2 sangat bagus, sayang cuaca kurang baik sehingga...</p>
                    <div class="font-medium underline py-1">
                        <a class="cursor-pointer">
                            Tampilkan lebih banyak <span><img src="/svg/chevronn-up.svg" alt="" class="h-4 inline rotate-90"></span>
                        </a>
                    </div>
                </div>
                <div class="flex flex-col">
                    <div class="flex items-center gap-2">
                        <span><img src="/svg/user.svg" alt="" class="h-10"></span>
                        <div>
                            <h1 class="font-medium">Indra</h1>
                            <h2 class="text-slate-600">September 2021</h2>
                        </div>
                    </div>
                    <p class="">Pengalaman menginap di veluvana sangat memuaskan, apa yang disampaikan di deskripsi dan foto sesuai.
                        Terutama View dr lantai 2 sangat bagus, sayang cuaca kurang baik sehingga...</p>
                    <div class="font-medium underline py-1">
                        <a class="cursor-pointer">
                            Tampilkan lebih banyak <span><img src="/svg/chevronn-up.svg" alt="" class="h-4 inline rotate-90"></span>
                        </a>
                    </div>
                </div>
                <div class="flex flex-col">
                    <div class="flex items-center gap-2">
                        <span><img src="/svg/user.svg" alt="" class="h-10"></span>
                        <div>
                            <h1 class="font-medium">Indra</h1>
                            <h2 class="text-slate-600">September 2021</h2>
                        </div>
                    </div>
                    <p class="">Pengalaman menginap di veluvana sangat memuaskan, apa yang disampaikan di deskripsi dan foto sesuai.
                        Terutama View dr lantai 2 sangat bagus, sayang cuaca kurang baik sehingga...</p>
                    <div class="font-medium underline py-1">
                        <a class="cursor-pointer">
                            Tampilkan lebih banyak <span><img src="/svg/chevronn-up.svg" alt="" class="h-4 inline rotate-90"></span>
                        </a>
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
            isShortDetail: false
        }
    },

}
</script>