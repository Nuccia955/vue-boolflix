<template>
    <li class="movie">
        <ul>
            <li>{{ movieTitle }}</li>
            <li>{{ movieOriginalTitle }} </li>
            <li>{{ movieLanguage }}</li>
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
    }
}
</style>