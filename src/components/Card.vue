<template>
    <li class="card">
        <div class="cover">
            <img :src="`https://image.tmdb.org/t/p/w185${img}`" :alt="title">
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
                <p>{{ overview }}</p>
            </li>
            <li>
                Voto:
                <span class="star" 
                    v-for="(star,index) in stars" 
                    :key="`star-${index}`" 
                >
                    <i class="fas fa-star"></i>
                </span>
                <span v-for="(star, index) in (5 - stars)" 
                    :key="`voidstar-${index}`"
                >
                    <i class="far fa-star"></i>
                </span>
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
            stars: Math.ceil(this.voteAverage / 2),
        }
    },
    computed: {
        availableFlag() {
            return this.flags.includes(this.language);
        },
    },
    props: {
        img: String,
        title: String,
        originalTitle: String,
        language: String,
        overview: String,
        voteAverage: Number,
    },
}
</script>

<style scoped lang="scss">
li.card {
    position: relative;
    margin: 30px 1px;
    min-width: calc(100% / 6 - 2px);
    .cover {
        width: 100%;
        img {
            width: 100%;
            display: block;
        }
    }
    ul {
        opacity: 0;
        transition: opacity 0.2s ease-in;
        &:hover {
            opacity: 1;
        }
        background-color: rgba(0, 0, 0, 0.5);
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        padding: 0 10px;
        overflow: auto;
        list-style: none;
        color: white;
        li {
            margin: 10px 0;
            font-size: 0.8rem;
            &.flag img {
                width: 30px;
                height: 15px;
                object-fit: cover;
            }
        }
    }
}
</style>