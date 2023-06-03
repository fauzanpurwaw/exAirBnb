
<template>
    <NuxtLayout :name="layouts.header" />
    <NuxtLayout :name="layouts.container"> 
        <IndexTax />
        <IndexDicouverz />
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
            },
        }
    }
}
</script>