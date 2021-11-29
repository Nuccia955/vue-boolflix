<template>
    <header>
        <input 
            type="text" 
            placeholder="Search movie or series"
            v-model="searchInput"
        >
        <button 
            @click="getMovieList"
        >
            Search
        </button>
    </header>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Header',
    data() {
        return {
            APIurl: 'https://api.themoviedb.org/3/search/movie',
            searchInput: '',
        }
    },
    methods: {
        getMovieList() {
            axios.get(this.APIurl, {
                params: {
                    api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                    query: `${this.searchInput}`,
                    language: 'it-IT',
                }
            })
            .then(response => {
                // handle success
                this.$emit('genMovieList', response.data.results)
                if(response.data.results.length > 0) {
                    this.$emit('errorMessage', '')
                } else {
                    this.$emit('errorMessage', 'Not Found')
                }
            })
            .catch(error => {
                // handle error
                this.$emit('errorMessage', `${error} ==> Please try again`);
            });
            this.searchInput = '';
        },
    }
}
</script>

<style scoped lang="scss">

</style>