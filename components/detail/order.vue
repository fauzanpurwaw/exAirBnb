<template>
    <div class="bg-white border border-gray-300 shadow-lg rounded-xl h-fit p-5 w-[372px] duration-1000 ">
        <div class="flex justify-between items-center">
            <h1 class="text-lg font-medium">$.{{ price }} <span class="font-normal text-slate-700">/pcs</span>
            </h1>
            <div class="flex gap-1 text-small">
                <div class="flex items-center">
                    <img src="../../public/svg/star.svg" alt="" class="h-4 mr-1">
                    <span class="">{{ rating }}</span>
                </div>
                -
                <div class="flex items-center gap-1">
                    {{ stock }}
                    <span class="text-slate-500 font-semibold">Stock</span>
                </div>
            </div>
        </div>
        <div class="flex mt-5 duration-1000">
            <div class="flex flex-col w-full border-gray-400 rounded-lg duration-1000">
                <div class="flex justify-between w-full h-full rounded-lg">
                    <div class="flex justify-center shadow-lg hover:shadow-xl items-center h-full flex-col w-full hover:scale-105 rounded-tl-lg hover:cursor-pointer"
                        @click="accumulateStock(-1, stock)">
                        <h1 class="text-[25px] text-left font-bold">-</h1>
                    </div>
                    <input type="number"
                        class="flex text-lg py-5 text-center justify-center items-center h-full flex-col w-full"
                        v-model="stockCounter" :on-keyup="accumulateStock(0, stock)" />
                    <div class="flex justify-center shadow-lg items-center h-full flex-col w-full hover:scale-105 rounded-tr-lg hover:cursor-pointer"
                        @click="accumulateStock(1, stock)">
                        <h1 class="text-[20px] text-left font-bold">+</h1>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex items-center py-8 bg-white h-8 w-fit px-1">
            <label for="note" class="text-rose-500 font-semibold mr-2 w-full cursor-pointer hover:scale-95 duration-100"
                @click="openNote = !openNote"> <span><img src="/svg/note.svg" alt="" class="h-6 inline mb-1"></span> Add
                note</label>
            <input type="text" id="note" name="note" placeholder="Contoh: warna putih, ukurann Xl"
                class="ring-1 ring-rose-500 h-8 rounded-lg w-64 text-slate-800 px-2" v-show="openNote">
        </div>
        <div
            class="active:scale-95 flex justify-center items-center rounded-lg bg-rose-500 h-12 cursor-pointer duration-100">
            <h1 class="text-white font-semibold">Buy now</h1>
        </div>
        <div @click="addToCart(id, stockCounter)"
            class="active:scale-95 border border-rose-500 flex justify-center items-center rounded-lg mt-4 bg-whit h-12 cursor-pointer duration-100">
            <h1 class="text-rose-500 font-semibold">+add to cart</h1>
        </div>
        <div class="flex justify-center items-center text-sm text-slate-500 mt-4">
            Anda belum dikenakan biaya
        </div>
        <div class="flex flex-col gap-4 mt-4 pb-6 border-gray-300 border-b">
            <div class="flex justify-between w-full">
                <div class="text-slate-600 underline cursor-pointer" @click="togglePriceDetail()">
                    $.{{ price }} x {{ stockCounter }} pcs
                </div>
                <div>
                    $.{{ price * stockCounter }}
                </div>
            </div>
            <Transition>
                <div class="flex flex-col shadow-lg border rounded-lg h-fit w-[330px] absolute top-[120px] duration-1000"
                    v-show="openPriceDetail">
                    <div class="flex fixed h-screen w-screen top-0 z-[1] left-0" @click="togglePriceDetail()"></div>
                    <div class="flex justify-end px-4 py-2 z-[2] bg-white rounded-t border shadow">
                        <button @click="togglePriceDetail()"
                            class="h-5 relative right-0 top-0 hover:scale-105 duration-300">
                            <img src="/svg/close.svg" alt="" class="h-full">
                        </button>
                    </div>
                    <div class="flex justify-center flex-col px-4 border shadow bg-white z-[2]">
                        <div class="flex justify-center text-small font-semibold mb-4 pt-4">
                            Perincian Harga Dasar
                        </div>
                        <div class="flex justify-between text-small mb-4">
                            <p>
                                {{ title }}
                            </p>
                            <p class="font-medium">
                                x {{ stockCounter }}pcs
                            </p>
                        </div>
                    </div>
                    <div class="flex justify-between text-small font-bold py-4 px-4 rounded-b border shadow bg-white z-[2]">
                        <p>
                            Total Harga Dasar
                        </p>
                        <p>
                            $.{{ price * stockCounter }}
                        </p>
                    </div>
                </div>
            </Transition>
            <div class="flex justify-between">
                <div class="text-slate-600 underline cursor-pointer" @click="toggleCleaninTax()">
                    Biaya pengemasan
                </div>
                <div>
                    $.{{ stockCounter == 0 ? 0 : cleaningPrice }}
                </div>
            </div>
            <Transition>
                <div class="absolute top-[260px] duration-1000" v-show="openCleaninTax">
                    <div class="fixed h-screen w-screen top-0 right-0 z-[1]" @click="toggleCleaninTax()"></div>
                    <div
                        class="flex items-center h-fit w-[330px] gap-4 p-2 bg-white absolute z-[2] border shadow-lg rounded-lg">
                        <button @click="toggleCleaninTax()" class="w-12 hover:scale-105 duration-300"><img
                                src="/svg/close.svg" alt="" class="h-full"></button>
                        <p class="text-sm text-slate-500 py-2">Biaya satu kali yang dikenakan tuan rumah untuk menutup biaya
                            membersihkan tempat mereka.
                        </p>
                    </div>
                </div>
            </Transition>
            <div class="flex justify-between">
                <div class="text-slate-600 underline cursor-pointer" @click="toggleAdminTax()">
                    Biaya layanan Airbnb
                </div>
                <Transition>
                    <div class="absolute top-[280px] duration-1000" v-show="openAdminTax">
                        <div class="fixed h-screen w-screen top-0 right-0 z-[1]" @click="toggleAdminTax()"></div>
                        <div
                            class="flex items-center h-fit w-[332px] gap-4 p-2 bg-white absolute z-[2] border shadow-lg rounded-lg">
                            <button @click="toggleAdminTax()" class="w-12 hover:scale-105 duration-300"><img
                                    src="/svg/close.svg" alt="" class="h-full"></button>
                            <p class="text-sm text-slate-500 py-2">Ini akan membantu kami membiayai pengoperasian platform
                                dan menyediakan layanan seperti dukungan 24/7 pada perjalanan Anda.</p>
                        </div>
                    </div>
                </Transition>
                <div>
                    $.{{ stockCounter == 0 ? 0 : adminPrice }}
                </div>
            </div>
        </div>
        <div class="flex justify-between mt-4 font-semibold">
            <div>
                Total sebelum pajak
            </div>
            ${{ stockCounter == 0 ? 0 : (price * stockCounter) + cleaningPrice + adminPrice }}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        id: {
            type: Number,
            default: 0
        },
        title: {
            type: String,
            default: ""
        },
        price: {
            type: Number,
            default: 0
        },
        stock: {
            type: Number,
            default: 0
        },
        rating: {
            type: Number,
            default: 0
        },
    },
    data() {
        return {
            stockCounter: 1,
            openPriceDetail: false,
            openCleaninTax: false,
            openAdminTax: false,
            cleaningPrice: 3.4,
            adminPrice: 11.1,
            openNote: false,
        }
    },
    methods: {
        togglePriceDetail() {
            this.openPriceDetail = !this.openPriceDetail;
            console.log(this.openPriceDetail);
        },
        toggleCleaninTax() {
            this.openCleaninTax = !this.openCleaninTax;
            console.log(this.openCleaninTax);
        },
        toggleAdminTax() {
            this.openAdminTax = !this.openAdminTax;
            console.log(this.openAdminTax);
        },
        accumulateStock(n, stock) {
            if (n == 1) {
                if (this.stockCounter < stock) {
                    this.stockCounter += n;
                } else if (this.stockCounter >= stock) {
                    this.stockCounter = stock;
                }
            } else if (n == -1) {
                if (this.stockCounter < 1) {
                    this.stockCounter = 1;
                } else if (this.stockCounter > 1) {
                    this.stockCounter += n;
                }
            } else if (this.stockCounter > stock) {
                this.stockCounter = stock;
            } else if (this.stockCounter < 1) {
                this.stockCounter = 1;
            }
            console.log(this.stockCounter, stock);
        },
        async addToCart(id, qty) {
            let { data: product }  = await useFetch('https://dummyjson.com/products/' + id);
            let dataProduct        = product._rawValue;
            dataProduct.qty        = qty;
            dataProduct.noteStatus = false;

            //if localStorage products didn't exist
            if (!localStorage.getItem("products")) {
                let array = [];
                dataProduct.cartId = 1;
                dataProduct.subTotal = (this.price * this.stockCounter) + this.cleaningPrice + this.adminPrice;
                array.push(dataProduct);
                localStorage.setItem("products", JSON.stringify(array));
                console.log(JSON.parse(localStorage.getItem("products")));
            } 
            //if localStorage products is exist
            else {
                //get all data from localStorage
                let productAtCart = JSON.parse(localStorage.getItem("products"));
                let listProductId = [];
                //get ListProductId in localStorage
                for (let i = 0; i < productAtCart.length; i++) {
                    if (!listProductId.includes(productAtCart[i].id)) {
                        listProductId.push(productAtCart[i].id)
                    }
                }
                console.log(listProductId);
                
                //check if the id already exists or not
                if (!listProductId.includes(dataProduct.id)) {
                    //if not exist save to localStorage
                    dataProduct.cartId   = productAtCart.length + 1;
                    dataProduct.subTotal = (this.price * this.stockCounter) + this.cleaningPrice + this.adminPrice;
                    productAtCart.push(dataProduct);
                    localStorage.setItem("products", JSON.stringify(productAtCart));
                    console.log(JSON.parse(localStorage.getItem("products")));
                    console.log(listProductId);
                } else {
                    //if exist
                    //get data with the same id from localStorage
                    for (let j = 0; j < productAtCart.length; j++) {
                        //if data found
                        if (productAtCart[j].id === id) {
                            productAtCart[j].subTotal += (this.price * this.stockCounter) + this.cleaningPrice + this.adminPrice;
                            productAtCart[j].qty      += qty;
                            localStorage.setItem("products", JSON.stringify(productAtCart));
                            console.log(JSON.parse(localStorage.getItem("products")));
                        }
                    }
                }
                console.log(JSON.parse(localStorage.getItem("products")));
            }
        }
    },
    mounted() {

    }
}
</script>