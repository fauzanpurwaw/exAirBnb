<template>
    <div class="flex justify-center w-full h-fit my-6">
        <div class="flex justify-between items-center min-w-[480px] sm:w-[500px] w-full bg-white rounded-full p-4 px-8 border border=slate-500">
            <div class="flex">
                <div class="flex sm:text-base text-sm font-semibold pr-4 border-r border-slate-400">
                    Display total price
                </div>
                <div class="flex sm:text-base text-sm pl-4 text-slate-500">
                    Includes all fees, before taxes
                </div>
            </div>
            <div class="flex">
                <div v-if="displayTotal" class="flex w-12 rounded-full bg-gray-300 p-[3px] hover:cursor-pointer duration-1000" @click="displayTotal = !displayTotal">
                    <div class="flex h-6 w-6 bg-white rounded-full duration-1000">
                        
                    </div>
                </div>
                <div v-else class="flex justify-end w-12 rounded-full bg-black p-[3px] hover:cursor-pointer duration-1000"  @click="displayTotal = !displayTotal">
                    <div class="flex h-6 w-6 p-1 bg-white rounded-full duration-1000">
                        <img src="/svg/check.svg" alt="" class="select-none h-full">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                displayTotal: true,
            }
        }
    }
</script>