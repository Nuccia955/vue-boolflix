<template>
    <li class="movie">
        <ul>
            <li>{{ movieTitle }}</li>
            <li>{{ movieOriginalTitle }} </li>
            <li>
                <img 
                    v-if="movieLanguage === 'en' || movieLanguage === 'it'" 
                    :src="require(`../assets/${movieLanguage}.png`)" :alt="movieLanguage"
                >
                <span v-else>{{ movieLanguage }}</span>
            </li>
            <li>{{ movieVote }}</li>
        </ul>
    </li>
</template>

<script>
export default {
    name: 'Movie',
    props: {
        movieTitle: String,
        movieOriginalTitle: String,
        movieLanguage: String,
        movieVote: String,
    },
}
</script>

<style scoped lang="scss">
li.movie {
    margin: 50px 0;
    ul {
        list-style: disc;
        li {
            margin-bottom: 5px;
            img {
                max-width: 30px;
            }
        }
    }
}
</style>