<template>
    <section class="list">
        <ul>
            <Card  
                v-for="item in list" 
                :key="`movie ${item.id}`"
                :title="item.title"
                :originalTitle="item.original_title"
                :language="item.original_language"
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
