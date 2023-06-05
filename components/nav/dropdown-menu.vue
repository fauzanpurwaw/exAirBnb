<template>
    <div class="flex flex-col">
        <button @click="dropdownOpen = !dropdownOpen"
            class="flex flex-row items-center filter min-w-fit h-6 py-5 px-2 border border-gray-300 rounded-full font-normal shadow-sm hover:shadow-lg z-[2]">
            <img src="/svg/menu.svg" alt="" class="h-5 mx-1">
            <img src="/svg/user.svg" alt="" class="h-7 mx-1">
        </button>
        <div class="absolute w-screen h-screen top-0 right-0 bottom-0" 
        v-show="dropdownOpen"
        >
        <div class="absolute w-screen h-screen z-[1]" @click="dropdownOpen = !dropdownOpen"></div>
            <ul id="ddMenu"
                class="absolute z-[2] w-[230px] font-normal text-slate-600 top-[64px] sm:right-10 right-0 bg-white p-5 visible rounded-lg">
                <li class="mb-5 hover:text-slate-800 "><NuxtLink to="/login">Login</NuxtLink></li>
                <li class="mb-5 hover:text-slate-800"><a href="" @click="logout()">Logout</a></li>
                <li class="pt-5 hover:text-slate-800 border-t"><NuxtLink to="/cart"><span><img src="/svg/cart.svg" alt="" class="h-4 inline mb-1 mr-2"></span>My cart</NuxtLink></li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            dropdownOpen: false
        }
    },
    methods: {
        logout() {
            localStorage.removeItem('user');
        }
    }
}
</script>