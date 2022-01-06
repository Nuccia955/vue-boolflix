<template>
    <section class="list">
        <h2>{{ sectionTitle }}</h2>
        <span v-if="searchInput"> 
            <strong>{{ list.length }}</strong>
            results found for
            <strong>{{ searchInput }}</strong>
        </span>
        <ul v-if="list.length > 0"
            @wheel.prevent="scrollingY"    
            :class="`show-case ${type}`"
        >
            <Card
                v-for="(item) in list"
                :type="type"
                :key="item.id"
                :id="item.id"
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
        type: String,
        searchInput: String,
    },
    components: {
        Card,
    },
    methods: {
        scrollingY(e) {
            if(e.wheelDelta > 0) {
                document.querySelector(`.show-case.${this.type}`).scrollLeft -= 100
            } else {
                document.querySelector(`.show-case.${this.type}`).scrollLeft += 100
            }
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
