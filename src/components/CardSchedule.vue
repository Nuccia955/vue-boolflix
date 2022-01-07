<template>
    <div class="schedule">
        <div class="btn close"
            @click="$emit('performCloseBtn')"
        >
            <i class="far fa-times-circle"></i>
        </div>
        <h2 class="title">
            {{ title }}
        </h2>
        <span class="adult" v-if="adult !== null && adult !== undefined">
            <i class="fas fa-circle"
                :class="[{green : adult === false}, red]"
            ></i>
        </span>
        <span class="release-date">
            {{ releaseDate }}
        </span>
        <div class="genres">
            Genres:
            <span v-for="(genre, index) in genres"
                :key="genre.id"
            >
                {{ genre.name }} 
                <span v-if="index !== genres.length - 1">, </span>
                <span v-else>.</span>
            </span>
        </div>
        <div class="btn expandCast"
            @click="activeExpandCast = !activeExpandCast"
        >
            <span v-if="activeExpandCast === false">See Cast</span>
            <span v-else>Hide Cast</span>
        </div>
        <div class="cast"
            v-if="activeExpandCast"
        >
            <span v-for="(actor, index) in cast"
                :key="actor.id"
            >
                {{ actor.original_name}}
                <span v-if="index !== cast.length - 1">, </span>
                <span v-else>.</span>
            </span>
        </div>
        <span class="language">Language : {{ language }}</span>
        <p class="overview">
            {{ overview }}
        </p>
        <span class="voteaverage">Vote:
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
        </span>
    </div>
</template>

<script>
export default {
    name:"CardSchedule",
    data() {
        return {
            activeExpandCast: false,
            stars: Math.ceil(this.voteAverage / 2) 
        }
    },
    props: {
        title: String,
        genres: Array,
        cast: Array,
        overview: String,
        language: String,
        voteAverage: Number,
        releaseDate: String,
        adult: Boolean,
    },
}
</script>

<style scoped lang="scss">
.schedule {
    color: white;
    height: calc(100% + 100px);
    width: calc(100% + 100px);
    padding: 50px 40px;
    background-color: rgba(0,0,0,.8);
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-40%, -50%);
    z-index: 1;
    display: flex;
    flex-direction: column;
    overflow: auto;
    .btn.close {
        align-self: end;
        i {
            font-size: 2em;
            color:rgb(220, 26, 40);
            &:hover {
                transform: scale(1.2);
            }
        }
    }
    h2 {
        margin-bottom: 0.5em;
    }
    .adult .green {
        color: green;
    }
    .adult .red {
        color: red;
    }
    .genres {
        font-size: 0.8em;
        margin-bottom: 0.7em;
    }
    .btn.expandCast {
        align-self: end;
        background-color: rgb(220, 26, 40);
        &:hover {
            background-color: rgb(154, 38, 46);
        }
        margin-bottom: 0.7em;
        padding: 3px 15px;
        font-size: 0.9em;
        border-radius: 15px;
        color: white;
    }
    .cast {
        font-size: 0.8em;
    }
    p.overview,
    span.language,
    span.release-date,
    span.adult {
        font-size: 0.9em;
        margin-bottom: 0.7em;
    }
}
</style>