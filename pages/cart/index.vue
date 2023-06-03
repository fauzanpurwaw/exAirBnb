
<template>
    <NuxtLayout :name="layouts.header" />
    <NuxtLayout :name="layouts.container">
        <div class="flex items-center gap-3 mt-10 duration-1000">
            <NuxtLink to="/" class="flex items-center gap-1 hover:text-slate-800">
                <img src="/svg/home.svg" alt="" class="h-6 inline duration-500">
                home
            </NuxtLink>
            <img src="/svg/chevronn-up.svg" alt="" class="h-6 rotate-90 inline duration-500">
            <NuxtLink to="" class="flex items-center gap-1 hover:text-slate-800">
                Cart
            </NuxtLink>
        </div>
        <div class="flex sm:justify-between gap-10 justify-center h-fit w-full mt-12 px-2 duration-1000">
            <div class="flex flex-col w-full h-fit duration-1000">
                <div class="flex justify-between items-center duration-1000">
                    <h1 class="text-2xl font-semibold">My cart</h1>
                    <h1 class="text-xl text-slate-900 font-semibold cursor-pointer hover:text-rose-800 active:scale-95 duration-100" @click="deleteAllData()">Delete All</h1>
                </div>
                <div class="flex justify-center items-center h-80 text-xl animate-pulse text-rose-600" v-show="cartData.length === 0">
                    Add somtehing..
                </div>
                <div class="flex flex-col mt-6 mb-8 duration-1000">
                    <div class="flex flex-col py-2" v-for="cartProduct in cartData">
                        <div class="flex">
                            <div class="flex">
                                <img :src="cartProduct.thumbnail" alt="" class="h-20 object-cover aspect-square mx-1">
                                <div class="flex flex-col mx-6">
                                    <div class="flex w-full justify-between">
                                        <NuxtLink :to="'/detail/'+cartProduct.id">
                                            <h2 class="active:scale-95 duration-300">{{ cartProduct.title }}</h2>
                                        </NuxtLink>
                                    </div>
                                    <div class="flex items-center">
                                        <span
                                            class="text-[12px] bg-rose-700 rounded text-white font-semibold px-2 text-center w-fit">{{ cartProduct.discountPercentage }}%</span>
                                        <span class="px-1 text-sm text-slate-500"><del>${{ cartProduct.price }}</del></span>
                                        <span class="font-semibold">${{ cartProduct.price - (cartProduct.discountPercentage/100*cartProduct.price) }}</span>
                                    </div>
                                    <div class="flex items-center">
                                        <span class="flex items-center h-8 border shadow-lg hover:scale-105 active:scale-95 cursor-pointer rounded-tl-lg text-xl text-center px-4">-</span>
                                        <input type="text" class="text-slate-800 font-semibold text-center px-4 w-12" disabled v-model="cartProduct.qty"/>
                                        <span class="flex items-center h-8 border shadow-lg hover:scale-105 active:scale-95 cursor-pointer rounded-tr-lg text-xl text-center px-4">+</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="flex justify-between px-1">
                            <div class="flex gap-4 items-center">
                                <label :for="'cartId'+cartProduct.id" class="flex justify-center items-center w-20 py-4">
                                    <span class="text-[12px] font-bold text-rose-500 hover:cursor-pointer" @click="cartProduct.noteStatus = true" v-if="cartProduct.noteStatus === false">Tulis catatan</span>
                                    <span class="text-[12px] font-bold text-rose-500 hover:cursor-pointer" @click="cartProduct.noteStatus = false" v-else>Batal</span>
                                </label>
                                <input
                                v-show="cartProduct.noteStatus"
                                @focusout="cartProduct.noteStatus = false"
                                :id="'cartId'+cartProduct.id"
                                placeholder="Pastikan tidak ada data pribadi"
                                type="text" class="text-[12px] text-slate-600 bg-white w-full block rounded h-6 ring-1 ring-rose-500 px-1">
                            </div>
                            <div class="flex">
                                <span class="text-rose-600 font-semibold cursor-pointer hover:text-rose-800 active:scale-95 duration-100 ml-2" @click="deleteSingleItem(cartProduct.id)">Delete</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="lg:flex bg-blue-200 w-full hidden duration-1000">
            </div>
        </div>
    </NuxtLayout>
    <Footer />
</template>

<script>
export default {
    data() {
        return {
            layouts: {
                header: "header",
                container: "container"
            },
            noteStatus: false,
            cartData: [],
            allSubTotal: 0
        }
    },
    methods: {
        getCartData() {
            let rawData = JSON.parse(localStorage.getItem("products"));
            this.cartData = rawData;
            console.log(this.cartData)
        },
        deleteAllData() {
            localStorage.removeItem("products");
            this.getCartData();
        },
        deleteSingleItem(id) {
            for (let i=0; i<this.cartData.length; i++) {
                if ( this.cartData[i].id === id ) {
                    this.cartData.splice(i,1);
                    localStorage.setItem("products",JSON.stringify(this.cartData));
                    this.getCartData;
                }
            }
        }
    },
    mounted() {
        this.getCartData()
    }
}
</script>