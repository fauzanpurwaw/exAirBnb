<template>
    <div class="flex flex-col">
        <button @click="dropdownOpen = !dropdownOpen"
            class="flex flex-row items-center filter min-w-fit h-6 py-5 px-2 border border-gray-300 rounded-full font-normal shadow-sm hover:shadow-lg">
            <img src="/svg/menu.svg" alt="" class="h-5 mx-1">
            <img src="/svg/user.svg" alt="" class="h-7 mx-1">
        </button>
        <div class="absolute w-screen h-[100vh] -top-20 right-0 bottom-0" 
        v-show="dropdownOpen"
        @click="dropdownOpen = !dropdownOpen">
            <ul id="ddMenu"
                class="absolute w-[230px] font-normal text-slate-600 top-36 right-10 bg-white p-5 visible rounded-lg">
                <li class="mb-5 hover:text-slate-800 font-medium"><a href="">Daftar</a></li>
                <li class="mb-5 hover:text-slate-800 "><a href="">Masuk</a></li>
                <li class="pt-5 mb-5 hover:text-slate-800 border-t"><a href="">Jadikan rumah Anda Airbnb</a></li>
                <li class="hover:text-slate-800 "><a href="">Bantuan</a></li>
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
}
</script>