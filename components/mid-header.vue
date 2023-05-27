<template>
    <div class="flex items-center px-8 h-20 w-full sticky top-0 border-b bg-white z-10 text-slate-950">
        <div class="w-full flex justify-between px-2 mx-auto font-semibold text-lg">
            <div class="flex flex-row justify-center items-center" >  
                <img src="/svg/airbnb.svg" alt="BnBlogo" srcset="" class="h-8 lg:block hidden">
                <img src="/svg/airbnb-1.svg" alt="BnBlogo" srcset="" class="h-10 lg:hidden sm:block hidden mr-3">
                <!-- searchbar desktop -->
                <div class="lg:flex flex-row justify-center items-center 
                gap-2 h-full ml-10 px-5 text-sm border border-gray-300 rounded-full
                hover:shadow hover:cursor-pointer w-fit hidden font-normal">
                    <a class="border-r-2 pr-2">Ke mana saja</a>
                    <a class="border-r-2 pr-2">Minggu mana pun</a>
                    <a >Tambah tamu</a>
                    <span class="bg-red-bnb px-2 py-1 rounded-full"><img src="/img/magnifying-glass.png" alt=""  class="h-4 inline"></span>
                </div>
                <!-- searchbar mobile -->
                <div class="lg:hidden flex justify-between items-center border border-red-400 rounded-full sm:w-60 w-40 p-1 pl-3 text-small font-normal">
                    Cari disini...
                    <span class="flex items-center justify-center bg-red-bnb p-2 rounded-full"><img src="/img/magnifying-glass.png" alt=""  class="h-4 inline"></span>
                </div>
            </div>
            <div class="flex justify-between items-center gap-4 text-sm min-w-fit">
                <a href="" class="hidden lg:block ">Jadikan rumah Anda Airbnb</a>
                <a href="" class="ml-2 hidden sm:block "><span><img src="/svg/globe.svg" alt="" class="h-5 inline"></span></a>
                <DropdownMenu />
            </div>
        </div>
    </div>
</template>