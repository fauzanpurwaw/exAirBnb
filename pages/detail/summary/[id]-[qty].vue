<script setup>
const { id } = useRoute().params;
const { qty } = useRoute().params;
const { data: data } = await useFetch('https://dummyjson.com/products/' + id);
</script>

<template>
    <DetailHeader />
    <NuxtLayout :name="layouts.container">
        <div class="flex justify-between gap-16 w-full py-20">
            <div class="flex flex-col gap-8 w-full">
                <div class="flex gap-8 items-center">
                    <NuxtLink :to="'/detail/'+id">
                        <span><img src="/svg/chevronn-up.svg" alt="" class="h-6 inline -rotate-90"></span>
                    </NuxtLink>
                    <h1 class="text-3xl font-semibold">Submit order</h1>
                </div>
                <div class="flex flex-col gap-4 pl-14">
                    <h1 class="text-2xl font-semibold">Perjalanan anda</h1>
                    <div class="flex flex-col">
                        <div class="flex w-full justify-between items-center">
                            <h1 class="text-lg font-semibold">discount</h1>
                            <h1>{{ numberFormat(data.price - (data.discountPercentage/100*data.price)) }}</h1>
                        </div>
                    </div>
                    <div class="flex flex-col pb-8 border-b border-slate-300">
                        <div class="flex w-full justify-between items-center">
                            <h1 class="text-lg font-semibold">Quantity</h1>
                            <h1>{{ qty }} pcs</h1>
                        </div>
                    </div>
                    <div class="flex w-full py-2 pb-10 border-b border-slate-300">
                        <div class="flex w-full flex-col gap-6">
                            <h1 class="text-2xl font-semibold">Choose how to pay</h1>
                            <div class="flex flex-col w-full">
                                <!-- full pay -->
                                <div class="flex flex-col gap-1 border border-black rounded-t-lg p-4"
                                    v-if="payMethod.full == true">
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay in full</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-2 w-2 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">Pay the total ({{ numberFormat(data.price*qty - (data.price - (data.discountPercentage/100*data.price))) }}) now and you're all
                                        set.</p>
                                </div>
                                <div class="flex flex-col gap-1 border border-slate-300 rounded-t-lg p-4"
                                    @click="payMethod.full = true, payMethod.later = false" v-else>
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay in full</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-6 w-6 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">Pay the total ({{ numberFormat(data.price*qty - (data.price - (data.discountPercentage/100*data.price))) }}) now and you're all
                                        set.</p>
                                </div>
                                <!-- later pay -->
                                <div class="flex flex-col gap-1 border border-black rounded-b-lg p-4"
                                    v-if="payMethod.later == true">
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay part now, part later</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-2 w-2 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">{{ numberFormat((data.price*qty - (data.price - (data.discountPercentage/100*data.price)))/2) }} due today, {{ numberFormat((data.price*qty - (data.price - (data.discountPercentage/100*data.price)))/2) }} on Jun 30,
                                        2023. No extra fees. <span class="text-slate-800 font-medium underline">More
                                            info.</span></p>
                                </div>
                                <div class="flex flex-col gap-1 border border-slate-300 rounded-b-lg p-4"
                                    @click="payMethod.later = true, payMethod.full = false" v-else>
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay part now, part later</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-6 w-6 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">{{ numberFormat((data.price*qty - (data.price - (data.discountPercentage/100*data.price)))/2) }} due today, {{ numberFormat((data.price*qty - (data.price - (data.discountPercentage/100*data.price)))/2) }} on Jun 30,
                                        2023. No extra fees. <span class="text-slate-800 font-medium underline">More
                                            info.</span></p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="flex py-2" v-show="auth==false">
                        <div class="flex w-full flex-col gap-6">
                            <h1 class="text-2xl font-semibold">Log in here to submit order</h1>
                            <div class="flex flex-col w-full">
                                <label for="" class="flex flex-col p-2 rounded-t-lg border hidden"
                                    :class="[showCountry === true ? 'border-black' : 'border-slate-300']"
                                    @click="showCountry = !showCountry">
                                    <div class="flex items-center justify-between">
                                        <div class="flex flex-col">
                                            <p class="text-[12px] text-slate-400">Country/region</p>
                                            <h1>Indonesia (62+)</h1>
                                        </div>
                                        <span class=""><img src="/svg/chevronn-up.svg" alt="" class="h-5 rotate-180"></span>
                                    </div>
                                </label>
                                <div class="flex flex-col w-[550px] border border-slate-300 h-16 absolute bg-white bottom-[33px] overflow-y-scroll"
                                    v-show="showCountry == true">
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                </div>
                                <input required type="text" class="border w-full px-2 py-4 rounded-t-lg border-slate-300"
                                    placeholder="Username" v-model="username">
                                <input required type="password" class="border w-full px-2 py-4 rounded-b-lg border-slate-300"
                                    placeholder="Password">
                                <div class="flex justify-center items-center py-2 text-[12px]">
                                    We’ll call or text you to confirm your number. Standard message and data rates
                                    apply.<span class="underline">Privacy Policy</span>
                                </div>
                            </div>
                            <form action="" class="w-full">
                                <button
                                    class="bg-rose-500 py-3 rounded-lg font-semibold text-white active:scale-95 duration-100 w-full" @click="login()">Continue</button>
                            </form>
                            <div class="flex justify-between items-center w-full">
                                <div class="flex w-full h-0 border border-slate-300"></div>
                                <div class="flex px-2 text-[12px]">or</div>
                                <div class="flex w-full h-0 border border-slate-300"></div>
                            </div>
                            <div class="flex justify-between gap-6">
                                <div class="flex w-full h-14 active:scale-95 duration-100">
                                    <button
                                        class="flex justify-center items-center rounded-lg border border-slate-900 bg-white w-full text-center">
                                        <img src="/facebook.png" alt="" class="h-5">
                                    </button>
                                </div>
                                <div class="flex w-full h-14 active:scale-95 duration-100">
                                    <button
                                        class="flex justify-center items-center rounded-lg border border-slate-900 bg-white w-full text-center">
                                        <img src="/google.png" alt="" class="h-5">
                                    </button>
                                </div>
                                <div class="flex w-full h-14 active:scale-95 duration-100">
                                    <button
                                        class="flex justify-center items-center rounded-lg border border-slate-900 bg-white w-full text-center">
                                        <img src="/apple.png" alt="" class="h-5">
                                    </button>
                                </div>
                            </div>
                            <div class="flex w-full h-14 active:scale-95 duration-100">
                                <button
                                    class="flex justify-between items-center rounded-lg border border-slate-900 bg-white w-full text-center px-6">
                                    <img src="/svg/mail.svg" alt="" class="h-5">
                                    <p>Continue with email</p>
                                    <div class="h-5 w-5"></div>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="flex w-full justify-center">
                <div class="flex gap-6 flex-col w-[70%] h-fit sticky top-32 rounded-lg border shadow p-4">
                    <div class="flex gap-2 w-full pb-6 border-b border-slate-300">
                        <img :src="data.thumbnail" alt="" class="h-28 w-32 object-cover aspect-square rounded-lg">
                        <div class="flex flex-col justify-between">
                            <div class="flex flex-col">
                                <span class="text-[12px] text-slate-400">{{ data.category }}</span>
                                <h1 class="font-medium"><span><img src="/svg/lang.svg" alt=""
                                            class="h-4 inline mb-1 mr-1"></span>{{ data.title }}</h1>
                            </div>
                            <div class="flex items-center">
                                <span><img src="/svg/star.svg" alt="" class="h-3 inline mb-1 mr-1">{{ data.rating }}</span>
                            </div>
                        </div>
                    </div>
                    <div class="flex flex-col gap-4 w-full pb-6 border-b border-slate-300">
                        <h1 class="text-2xl font-medium">Price details</h1>
                        <div class="flex gap-3 flex-col text-slate-600">
                            <div class="flex justify-between">
                                <h1>{{ numberFormat(data.price) }} x {{ qty }} pcs</h1>
                                <h1>{{ numberFormat(data.price*qty) }}</h1>
                            </div>
                            <div class="flex justify-between">
                                <h1 class="underline cursor-pointer ">Total discount</h1>
                                <h1>{{ numberFormat((-(data.price - (data.discountPercentage/100*data.price)))) }}</h1>
                            </div>
                            <div class="flex justify-between">
                                <h1 class="underline cursor-pointer ">Airbnb service fee</h1>
                                <h1>{{ numberFormat(3.4) }}</h1>
                            </div>
                            <div class="flex justify-between">
                                <h1 class="underline cursor-pointer ">Taxes</h1>
                                <h1>{{ numberFormat(11.1) }}</h1>
                            </div>
                        </div>
                    </div>
                    <div class="flex w-full">
                        <div class="flex w-full justify-between text-lg font-semibold">
                            <h1>Total (USD)</h1>
                            <h1>{{ numberFormat(data.price*qty - (data.price - (data.discountPercentage/100*data.price)) + 3.4 + 11.1) }}</h1>
                        </div>
                    </div>
                    <div class="flex justify-center text-lg font-medium text-white bg-rose-500 rounded-lg py-4 cursor-pointer active:scale-95 duration-100" @click="showSuccess = true" v-show="auth==true">
                        Submit order
                    </div>
                </div>
            </div>
        </div>
        <div class="flex w-screen h-screen top-0 right-0 fixed justify-center items-center" v-show="showSuccess == true">
            <NuxtLink to="/" class="cursor-default">
                <div class="h-screen w-screen top-0 right-0 bg-black opacity-40 absolute z-[1]" @click="showSuccess = false">
                </div>
            </NuxtLink>
            <div class="bg-white w-80 rounded-lg shadow-lg z-[2] p-4">
                <NuxtLink to="/">
                    <img src="/svg/close.svg" alt="" class="h-6 hover:scale-105 cursor-pointer" @click="showSuccess = false">
                </NuxtLink>
                <div class="flex items-center flex-col py-4">
                    <img src="/add.gif" alt="">
                    <h1 class="text-xl font-semibold py-2">Order success!</h1>
                </div>
            </div>
        </div>
    </NuxtLayout>
<DetailFooter /></template>
<script>
export default {
    data() {
        return {
            layouts: {
                header: "header",
                container: "container"
            },
            payMethod: {
                full: false,
                later: false
            },
            showCountry: false,
            username: '',
            showSuccess: false,
            auth: false
        }
    },
    methods: {
        numberFormat(price) {
            return new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'USD',
            }).format(price)
        },
        login() {
            localStorage.setItem('user', this.username);
            this.auth = true;
        },
        checkAuth() {
            const user = localStorage.getItem('user');
            if (user) {
            console.log(localStorage.getItem('user'));
            this.auth = true;
            }
        }
    },
    mounted() {
        this.checkAuth();
    }
}
</script>