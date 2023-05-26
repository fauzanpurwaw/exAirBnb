<template>
    <button @click="filterOpen = true"
        class="flex flex-row items-center filter min-w-fit h-6 pl-3 pr-4 py-6 border border-gray-300 rounded-2xl font-normal">
        <img src="/svg/adjust.svg" alt="" class="h-5 mx-1">
        <p>Filter</p>
    </button>
    <Teleport to="body">
        <Transition>
        <div class="flex justify-center items-center w-full h-[100vh] z-50 bg-slate-700 bg-opacity-50 fixed"
            v-show="filterOpen">
                <div class="flex flex-col items-center bg-white h-[90vh] w-[760px] max-w-[800px] rounded-xl shadow-xl px-5">
                    <div class="flex items-center  bg-red-100 w-full h-[10%] rounded-t-xl relative">
                        <button @click="filterOpen = false" class="opacity-75 hover:opacity-100"><span><img src="/svg/close.svg" alt="" class="h-5"></span></button>
                        <div class="text-lg font-semibold w-full text-center mr-5">Filter</div>
                    </div>
                    <div class="border bg-red-200 h-[80%] w-full overflow-y-auto py-4">
                        <div>
                            <h2 class="text-2xl font-semibold text-slate-800">Price range</h2>
                            <p class="text-lg text-slate-600">The average nightly price is Rp1,145,983, not including fees or taxes.</p>
                            <div class="flex justify-center items-center w-full p-5 mt-5">
                                <input type="number" name="" id="" class="flex-1 w-full h-16 rounded-lg text-center">
                                <p class="mx-5">s/d</p>
                                <input type="number" name="" id="" class="flex-1 w-full h-16 rounded-lg text-center">
                            </div>
                        </div>
                        <div class="mt-10">
                            <h2 class="text-2xl font-semibold text-slate-800">Bed & Bedroom</h2>
                            <p class="text-lg text-slate-600">Beds</p>
                            <div class="flex items-center w-full p-5 mt-5">
                            </div>
                        </div>
                    </div>
                    <div class="bg-red-100 w-full h-[10%] rounded-b-xl">

                    </div>
                </div>
            </div>
        </Transition>
    </Teleport>
</template>

<script>
export default {
    props: {
        filterOpen: Boolean,
    }
}
</script>