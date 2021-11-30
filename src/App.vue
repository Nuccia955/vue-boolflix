<template>
    <div id="app">
        <Header @performSearch="getList" />

        <main class="w-100">
            <CardList
                sectionTitle="Movies"
                v-if="movieList"
                :list="this.movieList"
            />
            <CardList
                sectionTitle="Series"
                v-if="seriesList"
                :list="this.seriesList"
            />
            <h3 v-if="errorMessage"> {{ errorMessage }} </h3>
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
            }
            if(searchInput !== '') {
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
.w-50 {
  width: 50%;
}
.w-100 {
  width: 100vw;
}
main {
  display: flex;
}
</style>
