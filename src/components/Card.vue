<template>
    <li class="movie">
        <ul>
            <li v-if="originalTitle !== title">
                Titolo:
                {{ title }}
            </li>
            <li>
                Titolo Originale:
                {{ originalTitle }} 
            </li>
            <li>
                Lingua Originale:
                <img 
                    v-if="language === 'en' || language === 'it'" 
                    :src="require(`../assets/${language}.png`)" :alt="language"
                >
                <span v-else>{{ language }}</span>
            </li>
            <li>
                Voto:
                {{ voteAverage }}
            </li>
        </ul>
    </li>
</template>

<script>
export default {
    name: 'Card',
    props: {
        title: String,
        originalTitle: String,
        language: String,
        voteAverage: Number,
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