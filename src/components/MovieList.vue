<template>
    <section class="movie-list">
        <ul>
            <Movie  
                v-for="(movie, index) in list" 
                :key="`movie ${index}`"
                :movieTitle="`${movie.title}`"
                :movieOriginalTitle="`${movie.original_title}`"
                :movieLanguage="`${movie.original_language}`"
                :movieVote="`${movie.vote_count}`"
            />
        </ul>
    </section>
</template>

<script>
import Movie from '@/components/Movie.vue'
export default {
    name: 'MovieList',
    props: {
        list: Array,
    },
    components: {
        Movie,
    } 
}
</script>

<style scoped lang="scss">
    .movie-list {
        padding: 30px 10px;
        ul {
            list-style: none;
            padding: 0;
        }
    }
</style>
