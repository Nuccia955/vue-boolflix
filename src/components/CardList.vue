<template>
    <section class="list">
        <h3>{{ sectionTitle }}</h3>
        <ul v-if="list.length > 0">
            <Card  
                v-for="item in list" 
                :key="`movie ${item.id}`"
                :title="item.title || item.name"
                :originalTitle="item.original_title || item.original_name"
                :language="item.original_language"
                :voteAverage="item.vote_average"
            />
        </ul>
        <h4 v-else>Not found</h4>
    </section>
</template>

<script>
import Card from '@/components/Card.vue'
export default {
    name: 'CardList',
    props: {
        list: Array,
        sectionTitle: String,
    },
    components: {
        Card,
    } 
}
</script>

<style scoped lang="scss">
    .list {
        padding: 30px 10px;
        ul {
            list-style: none;
            padding: 0;
        }
    }
</style>
