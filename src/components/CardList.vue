<template>
    <section class="list">
        <h2>{{ sectionTitle }}</h2>
        <span v-if="searchInput"> 
            <strong>{{ list.length }}</strong>
            results found for
            <strong>{{ searchInput }}</strong>
        </span>
        <ul v-if="list.length > 0">
            <Card
                v-for="(item) in list"
                :genres="getGenres(item.id, type)"
                :key="item.id"
                :img="item.poster_path"
                :title="item.title || item.name"
                :originalTitle="item.original_title || item.original_name"
                :language="item.original_language"
                :overview="item.overview"
                :voteAverage="item.vote_average"
            />
        </ul>
    </section>
</template>

<script>
import axios from 'axios'
import Card from '@/components/Card.vue'
export default {
    name: 'CardList',
    props: {
        list: Array,
        sectionTitle: String,
        type: String,
        searchInput: String,
    },
    components: {
        Card,
    },
    methods: {
        getGenres(id, type) {
            console.log('id', id)
            axios.get(`https://api.themoviedb.org/3/${type}/${id}`, {
                params: {
                    api_key: '9523b234fd1c8550cfc9dea66c01f6f2',
                    langauge: 'it-IT',
                }
            })
            .then(response => {
                this.genres = response.data.genres
                console.log('genres', this.genres)
                return this.genres

            })
            .catch(error => {
                console.log(error)
            })
        }
    }
    
}
</script>

<style scoped lang="scss">
    .list {
        strong {
            color: rgb(220, 26, 40);
        }
        padding: 30px 10px;
        ul {
            width: 100%;
            list-style: none;
            padding: 0;
            display: flex;
            overflow-x: auto;
        }
    }
</style>
