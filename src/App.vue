<template>
    <div id="app">
        <Header @performSearch="getList" />

        <main>
            <CardList 
                v-if="movieList && this.errorMessage === ''"
                :list="this.movieList"
            />
            <h3 ref="errorMessage" v-else>{{ this.errorMessage }}</h3>
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
            movieList: null,
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
                    if(response.data.results.length > 0) {
                        this.errorMessage = '';
                    } else {
                        this.errorMessage = 'Not Found';
                    }
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

</style>
