<template>
    <TopHeader />
    <MidHeader />
    <BotHeader :dir="botDir"/>
</template>

<script>
    export default {
        props: {
            botDir: {
                type: String,
                default: "categories/"
            }
        }
    }
</script>