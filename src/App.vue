<template>
    <div id="app">
        <Header />

        <main>
            <MovieList />
        </main>
    </div> 
</template>

<script>
import Header from '@/components/Header.vue'
import MovieList from '@/components/MovieList.vue'
export default {
    name: 'App',
    components: {
        Header,
        MovieList,
    }
}
</script>

<style lang="scss">

</style>
