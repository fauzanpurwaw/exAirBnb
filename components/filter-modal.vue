<template>
    <button @click="filterOpen = true"
        class="flex flex-row items-center filter min-w-fit h-6 pl-3 pr-4 py-6 border border-gray-300 rounded-2xl font-normal">
        <img src="/svg/adjust.svg" alt="" class="h-5 mx-1">
        <p>Filter</p>
    </button>
    <Teleport to="body">
        <Transition>
            <div class="flex justify-center items-center w-full h-[100vh] z-20 fixed" v-show="filterOpen">
                <div class="relative h-full w-full flex items-center justify-center">
                    <div class="absolute h-screen w-screen bg bg-slate-700 bg-opacity-25 z-[1]"
                        @click="filterOpen = false, clearDataFilter()">
                    </div>
                    <div
                        class="flex flex-col items-center bg-white sm:h-[90vh] h-full w-full max-w-[800px] rounded-xl shadow-xl px-5 z-[2]">
                        <div class="flex items-center w-full h-[10%] border-b rounded-t-xl relative">
                            <div class="text-lg font-semibold w-full text-center ml-5">Filter</div>
                            <button @click="filterOpen = false, clearDataFilter()"
                                class="opacity-75 hover:opacity-100"><span><img src="/svg/close.svg" alt=""
                                        class="h-6"></span></button>
                        </div>
                        <div class="flex flex-col h-[80%] w-full overflow-y-auto py-4">
                            <div>
                                <h2 class="text-2xl font-semibold text-slate-800">Price range</h2>
                                <p class="text-lg text-slate-600 font-light">The average nightly price is Rp1,145,983, not
                                    including fees or taxes.</p>
                                <div class="flex justify-center items-center w-full p-5 mt-5">
                                    <input type="number" name="" id="" class="flex-1 w-full shadow h-16 rounded-lg text-center font-light border-2" v-model="priceRange.from">
                                    <p class="mx-5 text-slate-500">s/d</p>
                                    <input type="number" name="" id="" class="flex-1 w-full shadow h-16 rounded-lg text-center font-light border-2 " v-model="priceRange.to">
                                </div>
                            </div>
                            <div class="mt-10">
                                <h2 class="text-2xl font-semibold text-slate-800">Bed & Bedroom</h2>
                                <div>
                                    <p class="text-lg text-slate-600 font-light mt-5">Beds</p>
                                    <div action="" class="flex items-center gap-2 px-2 mt-3 flex-wrap">
                                        <div v-for="p in bedntoiletList">
                                            <label v-if="picked.bed == p" :for="p + 'bed'"
                                                class="flex justify-center border rounded-full px-3 py-2 text-center bg-black text-white cursor-pointer">
                                                <input type="radio" :value="p" :id="p + 'bed'" name="bed" class="invisible"
                                                    v-model="picked.bed">
                                                <p class="mr-4 font-light">{{ p }}</p>
                                            </label>
                                            <label v-else :for="p + 'bed'"
                                                class="flex justify-center border rounded-full px-3 py-2 text-center hover:border-black cursor-pointer duration-300">
                                                <input type="radio" :value="p" :id="p + 'bed'" name="bed" class="invisible"
                                                    v-model="picked.bed">
                                                <p class="mr-4 font-light">{{ p }}</p>
                                            </label>
                                        </div>
                                    </div>
                                </div>
                                <div>
                                    <p class="text-lg text-slate-600 font-light mt-5">Rest Room</p>
                                    <div action="" class="flex items-center gap-2 px-2 mt-3 flex-wrap">
                                        <div v-for="p in bedntoiletList">
                                            <label v-if="picked.toilet == p" :for="p + 'toilet'"
                                                class="flex justify-center border rounded-full px-3 py-2 text-center bg-black text-white cursor-pointer">
                                                <input type="radio" :value="p" :id="p + 'toilet'" name="toilet"
                                                    class="invisible" v-model="picked.toilet">
                                                <p class="mr-4 font-light">{{ p }}</p>
                                            </label>
                                            <label v-else :for="p + 'toilet'"
                                                class="flex justify-center border rounded-full px-3 py-2 text-center hover:border-black cursor-pointer duration-300">
                                                <input type="radio" :value="p" :id="p + 'toilet'" name="toilet"
                                                    class="invisible" v-model="picked.toilet">
                                                <p class="mr-4 font-light">{{ p }}</p>
                                            </label>
                                        </div>
                                    </div>
                                </div>
                                <div class="flex items-center w-full p-5 mt-5">
                                </div>
                            </div>
                            <div class="mt-10">
                                <h2 class="text-2xl font-semibold text-slate-800">Property type</h2>
                                <div class="mt-5 flex gap-5 flex-wrap" >
                                    <div class="flex gap-5 items-center" v-for="item in property.list">
                                        <div v-if="property.checked.includes(item.name)">
                                            <label :for="'type'+item.name" class="flex flex-col bg-black text-white justify-center items-start gap-3 border rounded-lg w-36 h-28 pl-3 hover:border-black duration-300 cursor-pointer" @click="uncheckType(item.name)">
                                            <img :src="'/svg/'+item.pict" alt="" class="h-10 p-2 rounded-full bg-white">
                                            <p class="font-semibold">{{ item.name }}</p>
                                        </label>
                                        <input type="checkbox" :name="'type'+item.name" :id="'type'+item.name" class="hidden">
                                        </div>
                                        <div v-else>
                                            <label :for="'type'+item.name" class="flex flex-col justify-center items-start gap-3 border rounded-lg w-36 h-28 pl-3 hover:border-black duration-300 cursor-pointer" @click="checkType(item.name)">
                                            <img :src="'/svg/'+item.pict" alt="" class="h-10">
                                            <p class="font-semibold">{{ item.name }}</p>
                                        </label>
                                        <input type="checkbox" :name="'type'+item.name" :id="'type'+item.name" class="hidden">
                                        </div>
                                        
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="flex justify-between items-center w-full h-[10%] rounded-b-xl border-t">
                            <div class="grid grid-cols-2 gap-4 w-full max-w-[580px]">
                                <div class="text-[12px]">
                                    Price Range : 
                                    <span class="font-semibold">Rp.{{ priceRange.from }}</span> 
                                    s/d 
                                    <span class="font-semibold">Rp.{{ priceRange.to }}</span> 
                                </div>
                                <div class="text-[12px]">
                                    Bed : 
                                    <span class="font-semibold">{{ picked.bed }}</span> 
                                </div>
                                <div class="text-[12px]">
                                    Property Type : 
                                    <div class="font-semibold inline" v-for="checkeed in property.checked">
                                    - {{ checkeed }}
                                    </div> 
                                </div>
                                <div class="text-[12px]">
                                    RestRoom : 
                                    <span class="font-semibold">{{ picked.toilet }} </span>
                                </div>
                            </div>  
                                <button @click="clearDataFilter" class=" font-semibold border border-black rounded-full px-5 py-1 text-xl hover:bg-black hover:text-white">Clear</button>
                        </div>
                    </div>
                </div>
            </div>
        </Transition>
    </Teleport>
</template>

<script>
export default {
    props: {
        filterOpen: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            bedntoiletList: ["bebas", "1", "2", "3", "4", "5", "6", "7", "8+"],
            picked: {
                bed: "bebas",
                toilet: "bebas",
            },
            priceRange: {
                from: 150000,
                to: 2800000
            },
            property: {
                list: [
                    {name: "Rumah", pict: "home.svg"},
                    {name: "Apartment", pict: "apartment.svg"},
                    {name: "Guesthouse", pict: "guest-house.svg"},
                ],
                checked: [],
            },
        }
    },
    methods: {
        clearDataFilter() {
            this.picked.bed = "bebas";
            this.picked.toilet = "bebas";
            this.property.checked = [];
            this.priceRange.from = 150000;
            this.priceRange.to = 2800000;
        },
        checkType(a) {
            if (!this.property.checked.includes(a)) {
                    this.property.checked.push(a);
                }
                // console.log(this.property.checked)
        },
        uncheckType(a) {
            for (let i=0; i<this.property.checked.length;i++) {
                if (this.property.checked[i] == a) {
                    this.property.checked.splice(i,1);
                    // console.log(a);
                    // console.log(this.property.checked);
                }
                // console.log(a);
                // console.log(this.property.checked);
            }
        }
    }
}
</script>