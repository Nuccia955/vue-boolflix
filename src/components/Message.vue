<template>
    <span> {{ this.getStarted }}</span>
</template>

<script>
export default {
    name: 'Message',
    data() {
        return {
            notFound: 'The movie/series you are looking for is not available',
            getStarted: 'Please type a movie/series title to start'
        }
    }
}
</script>

<style>

</style>