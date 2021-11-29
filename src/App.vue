<template>
    <div id="app">
        <Header @genMovieList="genList"
                @errorMessage="genErrorMessage" 
        />

        <main>
          <MovieList 
              v-if="movieList && this.errorMessage === ''"
              :list="this.movieList"
          />
          <h3 ref="errorMessage" v-else>{{ this.errorMessage }}</h3>
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
            errorMessage: null,
        }
    },
    components: {
        Header,
        MovieList,
    },
    methods: {
      genList(list) {
          this.movieList = list;
      },
      genErrorMessage(error) {
          this.errorMessage = `${error}`;
      }
    }
    
}
</script>

<style lang="scss">

</style>
