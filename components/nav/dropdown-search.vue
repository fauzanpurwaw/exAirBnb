
<template>
    <label for="searchInput" class="sm:flex flex-row justify-center items-center 
                    gap-2 h-full lg:ml-5 px-5 py-1 text-sm border border-gray-300 rounded-full
                    hover:shadow hover:cursor-pointer w-fit hidden font-normal" @click="toggleSearch = !toggleSearch, filterData(),keyWord = ''">
        <a class="border-r-2 pr-2">Butuh apa?</a>
        <a class="border-r-2 pr-2">Semua ada disini</a>
        <a>Cari semua disni</a>
        <span class="bg-red-bnb px-2 py-1 rounded-full">
            <img src="/img/magnifying-glass.png" alt="" class="h-4 inline">
        </span>
    </label>
    <!-- searchbar mobile -->
    <label for="searchInput"
        class="sm:hidden flex items-center justify-between border border-red-400 rounded-full w-full p-1 text-small font-normal hover:cursor-pointer"
        @click="toggleSearch = !toggleSearch, filterData(), keyWord = ''">
        <div class="flex h-ful justify-center items-center text-slate-400">
            <span class="flex items-center justify-center bg-red-bnb p-2 rounded-full mr-3">
                <img src="/img/magnifying-glass.png" alt="" class="h-5 inline">
            </span>
            Cari Disini...
        </div>
    </label>
    <Transition>
        <div class="flex h-screen w-screen absolute top-0 right-0 cursor-default" v-show="toggleSearch">
            <div class="absolute h-screen w-screen z-[1]" @click="toggleSearch = !toggleSearch, keyWord = ''"></div>
            <div
                class="relative flex bg-white h-fit sm:w-[400px] w-full py-3 px-2 lg:left-[162px] sm:left-[90px] left-0 sm:mx-0 mx-2 top-[5px] rounded-xl z-[99]">
                <div class="flex flex-col w-full overflow-y-auto">
                    <label for="searchInput">
                        <div
                            class="flex items-center justify-between border border-red-400 rounded-full w-full p-1 text-small font-normal">
                            <div class="flex h-full justify-center items-center">
                                <span class="flex items-center justify-center bg-red-bnb p-2 rounded-full mr-3">
                                    <img src="/img/magnifying-glass.png" alt="" class="h-5 inline">
                                </span>
                                <input type="text" name="" id="searchInput"
                                    class="py-1 px-3 sm:w-[300px] w-[35vh] text-small text-slate-500 accent-rose-400"
                                    placeholder="Cari Disini..." v-model="keyWord"
                                    @keyup="filterData()">
                            </div>
                            <button class="p-2 rounded-full hover:bg-rose-100 mx-1"
                                @click="toggleSearch = !toggleSearch"><img src="/svg/close.svg" alt="" class="h-5"></button>
                        </div>
                    </label>
                    <div class="flex flex-col w-full overflow-y-auto max-h-[600px]">
                        <div class="flex items-center w-full border-b px-2 py-2 hover:cursor-pointer hover:bg-rose-100 rounded mt-2"
                            v-for="product in productData.products" :key="product.id">
                            <NuxtLink :to="'detail/' + product.id">
                                <div class="flex items-center w-full border-b px-2 py-2 hover:cursor-pointer hover:bg-rose-100 rounded mt-2"
                                    id="list">
                                    <img src="/svg/user.svg" alt="" class="h-5">
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
                    let { data: data } = await useFetch('https://dummyjson.com/products/search?q='+this.keyWord.toLowerCase());
                        this.productData = data;
                        console.log(this.productData);
            }
        }
    },
}
</script>