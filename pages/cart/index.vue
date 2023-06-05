
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
                    <h1 class="text-xl text-slate-900 font-semibold cursor-pointer hover:text-rose-800 active:scale-95 duration-100"
                        @click="toggleDeleteAll = true">Delete All</h1>
                </div>
                <div class="flex justify-center items-center h-80 text-xl animate-pulse text-rose-600"
                    v-show="cartData.length == 0">
                    Add somtehing..
                </div>
                <div class="flex flex-col mt-6 mb-8 duration-1000">
                    <div class="flex flex-col py-2" v-for="cartProduct in cartData">
                        <div class="flex">
                            <div class="flex">
                                <img :src="cartProduct.thumbnail" alt="" class="h-20 object-cover aspect-square mx-1">
                                <div class="flex flex-col mx-6">
                                    <div class="flex w-full justify-between">
                                        <NuxtLink :to="'/detail/' + cartProduct.id">
                                            <h2 class="active:scale-95 duration-300">{{ cartProduct.title }}</h2>
                                        </NuxtLink>
                                    </div>
                                    <div class="flex items-center">
                                        <span
                                            class="text-[12px] bg-rose-700 rounded text-white font-semibold px-2 text-center w-fit">{{
                                                cartProduct.discountPercentage }}%</span>
                                        <span class="px-1 text-sm text-slate-500"><del>{{ numberFormat(cartProduct.price) }}</del></span>
                                        <span class="font-semibold">${{ cartProduct.netPrice }}</span>
                                    </div>
                                    <div class="flex items-center">
                                        <span
                                            class="flex items-center h-8 border shadow-lg hover:scale-105 active:scale-95 cursor-pointer rounded-tl-lg text-xl text-center px-4"
                                            @click="accumulateQty(cartProduct.id, -1, cartProduct.stock)">-</span>
                                        <input type="text" class="text-slate-800 font-semibold text-center px-4 w-16    "
                                            disabled v-model="cartProduct.qty" />
                                        <span
                                            class="flex items-center h-8 border shadow-lg hover:scale-105 active:scale-95 cursor-pointer rounded-tr-lg text-xl text-center px-4"
                                            @click="accumulateQty(cartProduct.id, 1, cartProduct.stock)">+</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="flex justify-between px-1">
                            <div class="flex gap-4 items-center">
                                <label :for="'cartId' + cartProduct.id" class="flex justify-center items-center w-20 py-4">
                                    <span class="text-[12px] font-bold text-rose-500 hover:cursor-pointer"
                                        @click="cartProduct.noteStatus = true" v-if="cartProduct.noteStatus === false">Tulis
                                        catatan</span>
                                    <span class="text-[12px] font-bold text-rose-500 hover:cursor-pointer"
                                        @click="cartProduct.noteStatus = false" v-else>Batal</span>
                                </label>
                                <input v-show="cartProduct.noteStatus" @focusout="cartProduct.noteStatus = false"
                                    :id="'cartId' + cartProduct.id" placeholder="Pastikan tidak ada data pribadi"
                                    type="text"
                                    class="text-[12px] text-slate-600 bg-white w-full block rounded h-6 ring-1 ring-rose-500 px-1">
                            </div>
                            <div class="flex">
                                <span
                                    class="text-rose-600 font-semibold cursor-pointer hover:text-rose-800 active:scale-95 duration-100 ml-2"
                                    @click="deleteSingleItem(cartProduct.id)">Delete</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="lg:flex justify-end w-full duration-1000 ">
                <div class="flex bg-white rounded-lg h-fit shadow-lg border w-96 sticky top-0 p-4 py-6">
                    <div class="flex flex-col gap-6 w-full">
                        <div class="flex w-full">
                            <div
                                class="border border-rose-500 cursor-pointer active:scale-95 duration-100 w-full h-fit rounded ">
                                <div class="flex justify-between py-2">
                                    <h1 class="text-slate-700 font-semibold ml-4">Save more using discount voucher</h1>
                                    <span><img src="/svg/chevronn-up.svg" alt="" class="inline h-6  rotate-90"></span>
                                </div>
                            </div>
                        </div>
                        <div class="flex flex-col pb-6 border-b border-slate-300">
                            <h1 class="text-lg  font-semibold text-slate-950 py-1">Summary</h1>
                            <div class="flex justify-between">
                                <h2 class="text-slate-600">Total price (0 barang)</h2>
                                <h2 class="text-slate-600">{{ numberFormat(allPrice) }}</h2>
                            </div>
                            <div class="flex justify-between">
                                <h2 class="text-slate-600">Total discount</h2>
                                <h2 class="text-slate-600">- {{ numberFormat(allDiscount) }}</h2>
                            </div>
                        </div>
                        <div class="flex justify-between">
                            <h1 class="text-xl font-semibold">Sub total</h1>
                            <h1 class="text-xl font-semibold">{{ numberFormat(allSubTotal) }}</h1>
                        </div>
                        <button class="bg-rose-500 text-white font-bold rounded-lg text-xl py-4"
                            :class="[allQty===0? 'bg-slate-300': '']"
                            :disabled="allQty===0"
                            @click="checkOut()">
                            Check out ({{ allQty }})
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </NuxtLayout>
    <Footer />
    <!-- modal -->
    <Transition>
        <div class="flex fixed top-0 right-0 justify-center items-center w-screen h-screen z-[999]"
            v-show="toggleDeleteAll === true">
            <div class="flex absolute h-screen w-screen top-0 right-0 bg-slate-800 opacity-50 z-[1]"
                @click="toggleDeleteAll = false"></div>
            <div class="flex flex-col justify-between w-[400px] h-64 rounded-lg p-4 bg-white z-[2]">
                <div class="flex justify-end">
                    <img src="/svg/close.svg" alt="" class="h-6 cursor-pointer hover:scale-105 active:scale-95"
                        @click="toggleDeleteAll = false">
                </div>
                <div class="flex flex-col items-center text-lg mb-8">
                    <div class="flex flex-col">
                        <img src="/delete.gif" alt="" class="w-24">
                    </div>
                    <div class="flex flex-col">
                        r u sure? want to delete this all?
                    </div>
                </div>
                <div class="flex justify-end">
                    <div class="flex gap-6">
                        <div class="text-rose-500 hover:scale-105 active:scale-95 font-medium cursor-pointer"
                            @click="toggleDeleteAll = false">
                            No
                        </div>
                        <div class="text-slate-700 hover:scale-105 active:scale-95 font-medium cursor-pointer"
                            @click="deleteAllData()">
                            Yes
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </Transition>
    <Transition>
        <div class="fixed h-screen w-screen top-0 right-0 flex justify-center items-center z-[99]" v-show="toggleCheckout === true">
            <div class="absolute h-screen w-screen z-[1] bg-black opacity-40" @click="toggleCheckout = false"></div>
            <div class="flex justify-between flex-col bg-white w-[40%] z-[2] p-4 py-10 rounded-lg shadow-lg border border-slate-300" @click="toggleCheckout = false">
                <img src="/svg/close.svg" alt="" class="h-6 w-6 hover:scale-105 cursor-pointer">
                <div class="flex flex-col items-center py-4">
                    <h1 class="text-3xl font-medium">Confirm your order</h1>
                    <p>r u sure want to check out all from cart? </p>
                </div>
                <div class="flex justify-between mt-4 px-[15%]">
                    <button class="text-rose-500 active:scale-95 duration-100" @click="toggleCheckout = false">
                        no
                    </button>
                    <button class="active:scale-95 duration-100" @click="confirm()">
                        yes
                    </button>
                </div>
            </div>
        </div>
    </Transition>
    <Transition>
        <div class="fixed h-screen w-screen top-0 right-0 flex justify-center items-center z-[99]" v-show="toggleLogin === true">
            <div class="absolute h-screen w-screen top-0 right-0 z-[1] bg-black opacity-40" @click="toggleLogin = false"></div>
            <div class="flex justify-between flex-col bg-white w-[40%] z-[2] p-4 py-10 rounded-lg shadow-lg border border-slate-300" @click="toggleLogin = false">
                <img src="/svg/close.svg" alt="" class="h-6 w-6 hover:scale-105 cursor-pointer">
                <div class="flex flex-col items-center py-4">
                    <h1 class="text-3xl font-medium">Login to confirm your order</h1>
                </div>
                <div class="flex justify-between mt-4 px-[15%]">
                    <button class="text-rose-500 active:scale-95 duration-100" @click="toggleLogin = false">
                        no
                    </button>
                    <NuxtLink to="/login">
                        <button class="active:scale-95 duration-100">
                            Login
                        </button>
                    </NuxtLink>
                </div>
            </div>
        </div>
    </Transition>
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
            allSubTotal: 0,
            allDiscount: 0,
            allPrice: 0,
            allQty: 0,
            toggleDeleteAll: false,
            toggleCheckout: false,
            toggleLogin: false,
        }
    },
    methods: {
        getCartData() {
            let rawData = JSON.parse(localStorage.getItem("products"));
            if (rawData) {
                this.cartData = rawData;
                console.log(this.cartData)
            } else {
                this.cartData = [];
                console.log(this.cartData)
            }
            this.setTotal();
        },
        deleteAllData() {
            this.cartData = [];
            localStorage.removeItem("products");
            this.toggleDeleteAll = false;
            this.getCartData();
        },
        deleteSingleItem(id) {
            for (let i = 0; i < this.cartData.length; i++) {
                if (this.cartData[i].id === id) {
                    this.cartData.splice(i, 1);
                    localStorage.setItem("products", JSON.stringify(this.cartData));
                    this.toggleDeleteAll = false;
                    // this.allQty =  this.allQty-this.cartData[i].qty;
                    // this.allPrice =  this.allPrice-(this.cartData[i].price*this.cartData[i].qty);
                    // this.allSubTotal =  this.allSubTotal-(this.cartData[i].netPrice*this.cartData[i].qty);
                    // this.allDiscount =  this.allDiscount-((this.cartData[i].price*this.cartData[i].qty)-(this.cartData[i].netPrice*this.cartData[i].qty));
                }
            }
            this.getCartData();
        },
        accumulateQty(id, qty, stock) {
            //get data with the same id
            for (let i = 0; i < this.cartData.length; i++) {
                if (this.cartData[i].id === id) {
                    if (qty == 1) {
                        if (this.cartData[i].qty < stock) {
                            this.cartData[i].qty += qty;
                        } else if (this.cartData[i].qty >= stock) {
                            this.cartData[i].qty = stock;
                        }
                    } else if (qty == -1) {
                        if (this.cartData[i].qty < 1) {
                            this.cartData[i].qty = 1;
                        } else if (this.cartData[i].qty > 1) {
                            this.cartData[i].qty += qty;
                        }
                    } else if (this.cartData[i].qty > stock) {
                        this.cartData[i].qty = stock;
                    } else if (this.cartData[i].qty < 1) {
                        this.cartData[i].qty = 1;
                    }
                    this.cartData[i].subTotal = this.cartData[i].qty * this.cartData[i].netPrice
                }
            }
            localStorage.setItem("products", JSON.stringify(this.cartData));
            this.getCartData();
        },
        setTotal() {
            if (!this.cartData.length == 0) {
                //set to 0
                this.allSubTotal = 0;
                this.allDiscount = 0;
                this.allPrice = 0;
                this.allQty = 0;
                for (let i = 0; i < this.cartData.length; i++) {
                    //then accumulate
                    this.allPrice += this.cartData[i].price * this.cartData[i].qty;
                    this.allSubTotal += this.cartData[i].netPrice * this.cartData[i].qty;
                    this.allDiscount += this.allPrice - this.allSubTotal;
                    this.allQty += this.cartData[i].qty;
                    console.log(this.allPrice);
                    console.log(this.allSubTotal);
                    console.log(this.allDiscount);
                }
            } else {
                this.allSubTotal = 0;
                this.allDiscount = 0;
                this.allPrice = 0;
                this.allQty = 0;
                console.log(this.allPrice);
                console.log(this.allSubTotal);
                console.log(this.allDiscount);
                console.log(this.allQty);
            }
        },
        numberFormat(price) {
            return new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'USD',
            }).format(price)
        },
        checkOut() {
            if ( localStorage.getItem('user') ) {
                this.toggleCheckout = true;
            } else {
                this.toggleLogin = true;
            }
        },
        confirm() {
            this.cartData = [];
            localStorage.removeItem("products");
            this.toggleCheckout = false;
            this.getCartData();
            alert('check out success');
        }
    },
    mounted() {
        this.getCartData()
    }
}
</script>