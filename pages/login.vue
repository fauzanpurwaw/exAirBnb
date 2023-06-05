<template>
    <div class="flex h-screen w-screen justify-center items-center">
        <div class="flex flex-col gap-4 border border-slate-200 rounded-lg p-4 py-10 shadow-lg shadow-gray-300 w-[30%]">
            <h1 class="text-2xl font-semibold text-slate-800 text-center">Welcome <span class="text-rose-500">guest!</span></h1>
            <form action="" class="flex flex-col gap-6 w-full items-center mt-6">
                <input type="text" placeholder="Username" class="w-[80%] rounded px-4 py-2 text-lg border border-b-rose-400 text-center" required v-model="username">
                <input type="password" placeholder="Password" class="w-[80%] rounded px-4 py-2 text-lg border border-b-rose-400 text-center" required>
                <div class="w-[80%] flex justify-end mt-6">
                        <button class="bg-rose-500 px-4 py-1 rounded text-lg font-semibold text-white active:scale-95 duration-100" @click="login()">
                            Login
                        </button>
                </div>
            </form>
        </div>
    </div>
    <!-- modal -->
    <Transition>
        <div class="fixed h-screen w-screen top-0 right-0 flex justify-center items-center" v-show="showInfo == true">
            <div class="absolute h-screen w-screen z-[1] bg-black opacity-40" @click="showInfo = false"></div>
            <div class="flex justify-between flex-col bg-white w-[40%] z-[2] p-4 py-10 rounded-lg shadow-lg border border-slate-300" @click="showInfo = false">
                <img src="/svg/close.svg" alt="" class="h-6 w-6 hover:scale-105 cursor-pointer">
                <div class="flex justify-center py-4">
                    <h1 class="text-3xl font-medium">You're already logged in</h1>
                </div>
                <div class="flex justify-between mt-4 px-[15%]">
                    <button class="text-rose-500 active:scale-95 duration-100" @click="logout()">
                        Log out
                    </button>
                    <NuxtLink to="/" class="active:scale-95 duration-100">
                        Go to home
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
                username: '',
                password: '',
                showInfo: false,
            }
        },
        methods: {
            login() {
                localStorage.setItem('user', this.username);
            },
            logout() {
                localStorage.removeItem('user');
            }
        },
        mounted() {
            if (localStorage.getItem('user')) {
                this.showInfo = true;
            }
        }
    }
</script>