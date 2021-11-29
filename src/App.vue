<template>
    <div id="app">
        <Header @genMovieList="genList"
                @errorMessage="genErrorMessage" 
        />

        <main>
          <h3 ref="errorMessage" v-if="this.errorMessage">{{ this.errorMessage }}</h3>
          <MovieList 
              :list="this.movieList"
          />
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
