<template>
    <div class="flex items-center sm:px-10 px-2 h-20 w-full sticky top-0 border-b bg-white z-10 text-slate-950">
        <div class="w-full flex justify-between mx-auto font-semibold text-lg">
            <div class="flex flex-row sm:justify-start items-center w-full" >  
                <NuxtLink to="/">
                    <img src="/svg/airbnb.svg" alt="BnBlogo" srcset="" class="h-8 lg:block hidden">
                </NuxtLink>
                <NuxtLink to="/">
                    <img src="/svg/airbnb-1.svg" alt="BnBlogo" srcset="" class="h-10 lg:hidden sm:block hidden mr-2">
                </NuxtLink>
                <!-- searchbar desktop -->
                <NavDropdownSearch />
                <NavDropdownMenu class="min-w-fit sm:hidden ml-3 text-small"/>
            </div>
            <div class="sm:flex justify-between items-center gap-4 text-sm min-w-fit hidden">
                <a href="" class="hidden lg:block ">Ingin menjual sesuatu?</a>
                <a href="" class="ml-2 hidden sm:block "><span><img src="/svg/globe.svg" alt="" class="h-5 inline"></span></a>
                <NavDropdownMenu />
            </div>
        </div>
    </div>
</template>