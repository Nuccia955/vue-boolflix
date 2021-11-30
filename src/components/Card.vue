<template>
    <li class="card">
        <ul>
            <li>
                <img :src="`https://image.tmdb.org/t/p/w92${img}`" :alt="title">
            </li>
            <li v-if="originalTitle !== title">
                Titolo:
                {{ title }}
            </li>
            <li>
                Titolo Originale:
                {{ originalTitle }} 
            </li>
            <li class="flag">
                Lingua Originale:
                <img 
                    v-if="availableFlag" 
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
    data() {
        return {
            flags: ['en', 'it'],
        }
    },
    computed: {
        availableFlag() {
            return this.flags.includes(this.language);
        }
    },
    props: {
        img: String,
        title: String,
        originalTitle: String,
        language: String,
        voteAverage: Number,
    },
}
</script>

<style scoped lang="scss">
li.card {
    margin: 50px 0;
    ul {
        list-style: disc;
        li {
            margin-bottom: 5px;
            &.flag img {
                max-width: 30px;
            }
        }
    }
}
</style>