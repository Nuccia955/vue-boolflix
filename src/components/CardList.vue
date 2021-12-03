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
                v-for="item in list" 
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
import Card from '@/components/Card.vue'
export default {
    name: 'CardList',
    props: {
        list: Array,
        sectionTitle: String,
        searchInput: String,
    },
    components: {
        Card,
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
