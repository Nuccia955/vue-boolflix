<template>
    <section class="movie-list">
        <ul>
            <Movie />
        </ul>
    </section>
</template>

<script>
import Movie from '@/components/Movie.vue'
export default {
    name: 'MovieList',
    components: {
        Movie,
    } 
}
</script>

<style scoped lang="scss">
    ul {
        list-style: none;
        padding: 0;
    }
</style>
