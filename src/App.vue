<template>
    <div id="app">
        <Header @genMovieList="genArray" />

        <main>
            <MovieList :list="this.movieList"/>
        </main>
    </div> 
</template>

<script>
import Header from '@/components/Header.vue'
import MovieList from '@/components/MovieList.vue'
export default {
    name: 'App',
    data() {
        return {
            movieList: null,
        }
    },
    components: {
        Header,
        MovieList,
    },
    methods: {
      genArray(list) {
          this.movieList = list;
          console.log(this.movieList);
      }
    }
    
}
</script>

<style lang="scss">

</style>
