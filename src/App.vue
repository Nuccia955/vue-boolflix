<template>
    <div id="app">
        <Header 
            @performSearch="getList"    
            @performTrendsOfTheWeek ="getTrends"
        />

        <Hero v-if="weeklyTrends"
            :list="weeklyTrends"
        />

        <main v-if="movieList || seriesList">
            <section class="lists">
                <CardList
                    sectionTitle="Movies"
                    type="movie"
                    v-if="movieList"
                    :list="this.movieList"
                    :searchInput="searchInput"
                />
                <CardList
                    sectionTitle="series"
                    type="series"
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
import Hero from '@/components/Hero.vue'

export default {
    name: 'App',
    data() {
        return {
            APIurlMovie: 'https://api.themoviedb.org/3/search/movie',
            APIurlSeries: 'https://api.themoviedb.org/3/search/tv',
            APIurlWeekTrends: 'https://api.themoviedb.org/3/trending/movie/week',
            weeklyTrends: null,
            movieList: null,
            seriesList: null,
            searchInput: null,
            errorMessage: null,
        }
    },
    components: {
        Header,
        CardList,
        Hero,
    },
    created() {
        this.getTrends();
    },
    methods: {
        getTrends() {
            this.movieList = null;
            this.seriesList = null;
            axios.get(this.APIurlWeekTrends, {
                params: {
                api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                langauge: 'it-IT',
                }
            })
            .then(response => {
                this.weeklyTrends = response.data.results.slice(0, 20);
            })
            .catch(error => {
                // handle error
                this.errorMessage = `${error} ==> Please again`;
            });
        },
        getList(searchInput) {
            this.weeklyTrends = null;
            if(searchInput !== '') {
                this.searchInput = searchInput;
                axios.get(this.APIurlMovie, {
                    params: {
                        api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                        query: searchInput,
                        langauge: 'it-IT'
                    },
                })
                .then(response => {
                    this.movieList = response.data.results
                })
                .catch(error => {
                    this.errorMessage = `${error} ==> Please try again`;
                })
                axios.get(this.APIurlSeries, {
                    params: {
                        api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                        query: searchInput,
                        langauge: 'it-IT',
                    },
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
::-webkit-scrollbar{
    width: .5em ;
    height: .5em ;
}    

::-webkit-scrollbar-track {
    background-color: rgb(154, 38, 46);
    border-radius: 0.50em;
    margin-block: 10px;
}

::-webkit-scrollbar-thumb {
    background-color:rgb(220, 26, 40);
    border-radius: 0.50em;
    margin-block: 10px;
}

@supports (scrollbar-color:rgb(220, 26, 40) rgb(154, 38, 46)) {
    * {
        scrollbar-color:rgb(220, 26, 40) rgb(154, 38, 46) ;
        scrollbar-width: thin;
    }
}
body {
  height: 100vh;
  color: white;
  margin: 0;
  background-color: rgb(33, 37, 41);
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    #app {
      height: 100%;
      font-family: sans-serif;
      cursor: default;
      main {
        padding: 50px 100px;
      }
    }
}
</style>
