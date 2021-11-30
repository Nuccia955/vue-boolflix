<template>
    <li class="card">
        <div class="cover">
            <img :src="`https://image.tmdb.org/t/p/w92${img}`" :alt="title">
        </div>
        <ul>
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
    display: flex;
    .cover {
        margin-right: 30px;
    }
    ul {
        flex-grow: 1;
        padding: 0;
        list-style: disc;
        li {
            margin-bottom: 10px;
            &.flag img {
                width: 30px;
                height: 15px;
                object-fit: cover;
            }
        }
    }
}
</style>