<template>
    <li class="movie">
        <ul>
            <li v-if="movieOriginalTitle !== movieTitle">
                Titolo:
                {{ movieTitle }}
            </li>
            <li>
                Titolo Originale:
                {{ movieOriginalTitle }} 
            </li>
            <li>
                Lingua Originale:
                <img 
                    v-if="movieLanguage === 'en' || movieLanguage === 'it'" 
                    :src="require(`../assets/${movieLanguage}.png`)" :alt="movieLanguage"
                >
                <span v-else>{{ movieLanguage }}</span>
            </li>
            <li>
                Voto:
                {{ movieVoteAverage }}
            </li>
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
        movieVoteAverage: String,
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