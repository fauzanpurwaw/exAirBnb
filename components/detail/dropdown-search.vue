<template>
    <label for="searchInput" class="md:flex flex-row justify-center items-center 
                    gap-2 h-full lg:ml-5 px-5 text-sm border border-gray-300 rounded-full
                    hover:shadow hover:cursor-pointer w-fit hidden font-normal py-1 max-w-[280px]"
        @click="toggleSearch = !toggleSearch, filterData(), keyWord = ''">
        <a class="border-r-2 pr-2 w-64">Cari disini...</a>
        <span class="bg-red-bnb px-2 py-1 rounded-full">
            <img src="/img/magnifying-glass.png" alt="" class="h-4 inline">
        </span>
    </label>
    <!-- searchbar mobile -->
    <!-- <label for="searchInput"
        class="sm:hidden flex items-center justify-between border border-red-400 rounded-full w-full p-1 text-small font-normal hover:cursor-pointer"
        @click="toggleSearch = !toggleSearch">
        <div class="flex h-full justify-center items-center text-slate-400">
            <span class="flex items-center justify-center bg-red-bnb p-2 rounded-full mr-3">
                <img src="/img/magnifying-glass.png" alt="" class="h-5 inline">
            </span>
            Cari Disini...
        </div>
    </label> -->
    <div class="flex w-full items-center justify-between md:hidden">
        <NuxtLink to="/" class="flex items-center text-small hover:underline">
            <img src="/svg/chevronn-up.svg" alt="" class="h-5 -ml-2 -rotate-90 mr-2">
            Rumah
        </NuxtLink>
        <div class="flex items-center justify-between gap-4">
            <NuxtLink to="" class="hover:cursor-pointer">
                <img src="/svg/upload.svg" alt="" class="h-4">
            </NuxtLink>
            <NuxtLink to="" class="hover:cursor-pointer">
                <img src="/svg/heart.svg" alt="" class="h-4">
            </NuxtLink>
        </div>
    </div>
    <Transition>
        <div class="flex h-screen w-screen absolute top-0 right-0 cursor-default duration-1000" v-show="toggleSearch">
            <div class="absolute h-screen w-screen z-[1]"
                @click="toggleSearch = !toggleSearch, filterData(), keyWord = ''"></div>
            <div
                class="relative flex bg-white h-fit md:w-[400px] w-full py-3 px-2 lg:left-[200px] sm:left-[90px] left-0 sm:mx-0 mx-2 top-[5px] rounded-xl z-[99]">
                <div class="flex flex-col w-full">
                    <label for="searchInput">
                        <div
                            class="flex items-center justify-between border border-red-400 rounded-full w-full p-1 text-small font-normal">
                            <div class="flex h-full justify-center items-center">
                                <span class="flex items-center justify-center bg-red-bnb p-2 rounded-full">
                                    <img src="/img/magnifying-glass.png" alt="" class="h-5 inline">
                                </span>
                                <input type="text" name="" id="searchInput"
                                    class="py-1 px-3 sm:w-[300px] w-[35vh] text-small text-slate-500 accent-rose-400"
                                    placeholder="Cari Disini..." v-model="keyWord" @keyup="filterData()">
                            </div>
                            <button class="p-2 rounded-full hover:bg-rose-100 mx-1"
                                @click="toggleSearch = !toggleSearch, keyWord = ''"><img src="/svg/close.svg" alt=""
                                    class="h-5"></button>
                        </div>
                    </label>
                    <div class="flex flex-col w-full overflow-y-auto max-h-[600px]">
                        <div class="flex items-center w-full border-b px-2 py-2 hover:cursor-pointer hover:bg-rose-100 rounded mt-2"
                            v-for="product in productData.products" :key="product.id">
                            <NuxtLink :to="'../detail/' + product.id">
                                <div class="flex items-center w-full border-b px-2 py-2 hover:cursor-pointer hover:bg-rose-100 rounded mt-2"
                                    id="list">
                                    <img :src="product.thumbnail" alt="" class="h-8 w-8">
                                    <p id="listItem" class="text-[12px] text-slate-500 mx-2">{{ product.title }} - {{
                                        product.brand }} - {{ product.category }}</p>
                                </div>
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </Transition>
</template>
<script>
export default {
    data() {
        return {
            toggleSearch: false,
            keyWord: "",
            productData: []
        }
    },
    methods: {
        async filterData() {
            if (this.keyWord === '') {
                let { data: data } = await useFetch('https://dummyjson.com/products?limit=5');
                this.productData = data;
                console.log(this.productData);
            } else {
                let { data: data } = await useFetch('https://dummyjson.com/products/search?q=' + this.keyWord.toLowerCase());
                this.productData = data;
                console.log(this.productData);
            }
        }
    },
}
</script>