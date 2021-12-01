<template>
    <div id="app">
        <Header @performSearch="getList" />

        <main>
            <section class="lists">
                <CardList
                    sectionTitle="Movies"
                    v-if="movieList"
                    :list="this.movieList"
                    :searchInput="searchInput"
                />
                <CardList
                    sectionTitle="Series"
                    v-if="seriesList"
                    :list="this.seriesList"
                    :searchInput="searchInput"
                />
            </section>
            <h3 class="w-100" v-if="errorMessage"> {{ errorMessage }} </h3>
        </main>
    </div> 
</template>

<script>
import axios from 'axios'
import Header from '@/components/Header.vue'
import CardList from '@/components/CardList.vue'
export default {
    name: 'App',
    data() {
        return {
            APIurlMovie: 'https://api.themoviedb.org/3/search/movie',
            APIurlSeries: 'https://api.themoviedb.org/3/search/tv',
            movieList: null,
            seriesList: null,
            searchInput: null,
            errorMessage: null,
        }
    },
    components: {
        Header,
        CardList,
    },
    methods: {
        getList(searchInput) {
            if(searchInput !== '') {
                this.searchInput = searchInput;
                axios.get(this.APIurlMovie, {
                    params: {
                        api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                        query: searchInput,
                        language: 'it-IT',
                    }
                })
                .then(response => {
                    // handle success
                    this.movieList = response.data.results;
                })
                .catch(error => {
                    // handle error
                    this.errorMessage = `${error} ==> Please try again`;
                });
                axios.get(this.APIurlSeries, {
                    params: {
                        api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                        query: searchInput,
                        language: 'it-IT',
                    }
                })
                .then(response => {
                    // handle success
                    this.seriesList = response.data.results;
                })
                .catch(error => {
                    // handle error
                    this.errorMessage = `${error} ==> Please try again`;
                });
            }
        },
    }
    
}
</script>

<style lang="scss">
#app {
  font-family: sans-serif;
  main {
    padding: 50px 100px;
    .lists {
      display: flex;
    }
  }
}
</style>
