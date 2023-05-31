<template>
    <div class="flex justify-center items-center mx-auto md:px-12 h-16 w-full max-w-[1280px] duration-1000 top-0 border-b bg-white z-10 text-slate-950">
        <div class="w-full flex justify-between md:px-0 px-4 mx-auto font-semibold text-lg">
            <div class="flex flex-row md:justify-start items-center w-full duration-1000" > 
                <NuxtLink to="/">
                    <img src="/svg/airbnb.svg" alt="BnBlogo" srcset="" class="min-h-8 h-8 lg:block hidden">
                </NuxtLink>
                <NuxtLink to="../">
                    <img src="/svg/airbnb-1.svg" alt="BnBlogo" srcset="" class="h-10 lg:hidden md:block hidden mr-4">
                </NuxtLink>
                <!-- searchbar desktop -->
                <DetailDropdownSearch />
            </div>
            <div class="md:flex justify-between items-center gap-4 text-sm min-w-fit hidden">
                <a href="" class="hidden md:block ">Jadikan rumah Anda Airbnb</a>
                <a href="" class="ml-2 hidden sm:block "><span><img src="/svg/globe.svg" alt="" class="h-5 inline"></span></a>
                <NavDropdownMenu />
            </div>
        </div>
    </div>
</template>