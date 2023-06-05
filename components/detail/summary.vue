<script setup>
    const { data: data } = await useFetch('https://dummyjson.com/products/' + id);
</script>
<template>
    <div class="flex justify-between gap-16 w-full py-20">
            <div class="flex flex-col gap-8 w-full">
                <div class="flex gap-8 items-center">
                    <span><img src="/svg/chevronn-up.svg" alt="" class="h-6 inline -rotate-90"></span>
                    <h1 class="text-3xl font-semibold">Submit order</h1>
                </div>
                <div class="flex flex-col gap-4 pl-14">
                    <h1 class="text-2xl font-semibold">Perjalanan anda</h1>
                    <div class="flex flex-col">
                        <div class="flex w-full justify-between items-center">
                            <h1 class="text-lg font-semibold">discount</h1>
                            <h2 class=" font-semibold underline">Edit</h2>
                        </div>
                        <h1>$111</h1>
                    </div>
                    <div class="flex flex-col pb-8 border-b border-slate-300">
                        <div class="flex w-full justify-between items-center">
                            <h1 class="text-lg font-semibold">Quantity</h1>
                            <h2 class=" font-semibold underline">Edit</h2>
                        </div>
                        <h1>{{ qty }}</h1>
                    </div>
                    <div class="flex w-full py-2 pb-10 border-b border-slate-300">
                        <div class="flex w-full flex-col gap-6">
                            <h1 class="text-2xl font-semibold">Choose how to pay</h1>
                            <div class="flex flex-col w-full">
                                <!-- full pay -->
                                <div class="flex flex-col gap-1 border border-black rounded-t-lg p-4" v-if="payMethod.full == true">
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay in full</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-2 w-2 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">Pay the total (Rp10,661,278.79) now and you're all set.</p>
                                </div>
                                <div class="flex flex-col gap-1 border border-slate-300 rounded-t-lg p-4" @click="payMethod.full = true, payMethod.later = false" v-else>
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay in full</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-6 w-6 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">Pay the total (Rp10,661,278.79) now and you're all set.</p>
                                </div>
                                <!-- later pay -->
                                <div class="flex flex-col gap-1 border border-black rounded-b-lg p-4" v-if="payMethod.later == true">
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay part now, part later</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-2 w-2 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">Rp5,760,095.07 due today, Rp4,901,183.72 on Jun 30, 2023. No extra fees. <span class="text-slate-800 font-medium underline">More info.</span></p>
                                </div>
                                <div class="flex flex-col gap-1 border border-slate-300 rounded-b-lg p-4" @click="payMethod.later = true, payMethod.full = false" v-else>
                                    <div class="flex w-full justify-between">
                                        <h2 class="font-medium">Pay part now, part later</h2>
                                        <div class="w-6 h-6 bg-black rounded-full flex justify-center items-center">
                                            <div class="h-6 w-6 bg-white border rounded-full cursor-pointer"></div>
                                        </div>
                                    </div>
                                    <p class="text-slate-600 w-[90%]">Rp5,760,095.07 due today, Rp4,901,183.72 on Jun 30, 2023. No extra fees. <span class="text-slate-800 font-medium underline">More info.</span></p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="flex py-2">
                        <div class="flex w-full flex-col gap-6">
                            <h1 class="text-2xl font-semibold">Log in or sign up to book</h1>
                            <div class="flex flex-col w-full">
                                <label for="" class="flex flex-col p-2 rounded-t-lg border " :class="[showCountry === true? 'border-black' : 'border-slate-300']" @click="showCountry = !showCountry">
                                    <div class="flex items-center justify-between">
                                        <div class="flex flex-col">
                                            <p class="text-[12px] text-slate-400">Country/region</p>
                                            <h1>Indonesia (62+)</h1>
                                        </div>
                                        <span class=""><img src="/svg/chevronn-up.svg" alt="" class="h-5 rotate-180"></span>
                                    </div>
                                </label>
                                <div class="flex flex-col w-[550px] border border-slate-300 h-16 absolute bg-white bottom-[-32px] overflow-y-scroll" v-show="showCountry == true">
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                    <div class="flex w-full px-3 hover:bg-blue-400 hover:text-white">Indonesia (+62)</div>
                                </div>
                                <input type="text" class="border w-full px-2 py-4 rounded-b-lg border-slate-300" placeholder="Phone number">
                                <div class="flex justify-center items-center py-2 text-[12px]">
                                    We’ll call or text you to confirm your number. Standard message and data rates apply.<span class="underline">Privacy Policy</span>
                                </div>
                            </div>
                            <button class="bg-rose-500 py-3 rounded-lg font-semibold text-white active:scale-95 duration-100">Continue</button>
                            <div class="flex justify-between items-center w-full">
                                <div class="flex w-full h-0 border border-slate-300"></div>
                                <div class="flex px-2 text-[12px]">or</div>
                                <div class="flex w-full h-0 border border-slate-300"></div>
                            </div>
                            <div class="flex justify-between gap-6">
                                <div class="flex w-full h-14 active:scale-95 duration-100">
                                    <button class="flex justify-center items-center rounded-lg border border-slate-900 bg-white w-full text-center">
                                        <img src="/facebook.png" alt="" class="h-5">
                                    </button>
                                </div>
                                <div class="flex w-full h-14 active:scale-95 duration-100">
                                    <button class="flex justify-center items-center rounded-lg border border-slate-900 bg-white w-full text-center">
                                        <img src="/google.png" alt="" class="h-5">
                                    </button>
                                </div>
                                <div class="flex w-full h-14 active:scale-95 duration-100">
                                    <button class="flex justify-center items-center rounded-lg border border-slate-900 bg-white w-full text-center">
                                        <img src="/apple.png" alt="" class="h-5">
                                    </button>
                                </div>
                            </div>
                            <div class="flex w-full h-14 active:scale-95 duration-100">
                                <button class="flex justify-between items-center rounded-lg border border-slate-900 bg-white w-full text-center px-6">
                                    <img src="/svg/mail.svg" alt="" class="h-5">
                                    <p>Continue with email</p>
                                    <div class="h-5 w-5"></div>
                                </button>
                            </div>
                        </div>
                    </div>
                    <!-- <input
                        type="email"
                        class="peer block min-h-[auto] w-full rounded border-0 bg-transparent px-3 py-[0.32rem] leading-[1.6] outline-none transition-all duration-200 ease-linear focus:placeholder:opacity-100 data-[te-input-state-active]:placeholder:opacity-100 motion-reduce:transition-none dark:text-neutral-200 dark:placeholder:text-neutral-200 [&:not([data-te-input-placeholder-active])]:placeholder:opacity-0"
                        id="exampleInputEmail1"
                        aria-describedby="emailHelp"
                        placeholder="Enter email" />
                    <label
                        for="exampleInputEmail1"
                        class="pointer-events-none absolute left-3 top-0 mb-0 max-w-[90%] origin-[0_0] truncate pt-[0.37rem] leading-[1.6] text-neutral-500 transition-all duration-200 ease-out peer-focus:-translate-y-[0.9rem] peer-focus:scale-[0.8] peer-focus:text-primary peer-data-[te-input-state-active]:-translate-y-[0.9rem] peer-data-[te-input-state-active]:scale-[0.8] motion-reduce:transition-none dark:text-neutral-200 dark:peer-focus:text-primary"
                        >Email address</label
                    > -->
                </div>
            </div>
            <div class="flex w-full  bg-blue-200">
                
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
            qty: {
                type: Number,
                default: 0
            }
        },
        data() {
            return {
                payMethod: {
                full: false,
                later: false
                },
                showCountry: false,
                data: []
            }
        },
    }
</script>