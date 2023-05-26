<template>
    <NuxtLayout :name="layouts.header" />
    <NuxtLayout :name="layouts.container">
        <Heibergement />
        <Explorer></Explorer>
        <Dicouverz />
        <Logement />
        <Experience />
        <Destination />
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
            }
        }
    }
}
</script>