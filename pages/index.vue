
<template>
    <NuxtLayout :name="layouts.header" />
    <NuxtLayout :name="layouts.container">
        <IndexOrder />
        <IndexHeibergement />
        <IndexExplorer />
        <IndexDicouverz />
        <IndexLogement />
        <IndexExperience />
        <IndexDestination />
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