
<template>
    <div>
        <div class="spinner-border text-primary" role="status">
        <span class="sr-only">Loading...</span>
        </div>{{ title }}
    </div>
</template>

<script>
    export default {
        name: 'loading',
        props: {
            title: String
        }
    }
</script>

<style lang="scss" scoped>

</style>