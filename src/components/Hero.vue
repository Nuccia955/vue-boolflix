<template>
    <section class="hero">
        <div class="trend"
            @mouseenter="stopAutoPlay"
            @mouseleave="autoPlay" 
        >
            <img :src="`https://image.tmdb.org/t/p/original${list[activeIndex].backdrop_path}`" :alt="`${list[activeIndex].title}`">
            <div v-if="stopSlider" class="trend-informations">
                <h2>{{ list[activeIndex].title || list[activeIndex].name  }}</h2>
                <div class="language-votes">
                    Lingua Originale:
                    <strong>{{ list[activeIndex].original_language }}</strong>
                    <span class="votes">
                        Voto:
                        <!-- <strong>{{ list[activeIndex].vote_average }}</strong> -->
                        <span class="star" 
                            v-for="(star,index) in Math.ceil(list[activeIndex].vote_average / 2)" 
                            :key="`star-${index}`" 
                        >
                            <i class="fas fa-star"></i>
                        </span>
                        <span v-for="(star, index) in (5 - Math.ceil(list[activeIndex].vote_average / 2))" 
                            :key="`voidstar-${index}`"
                        >
                            <i class="void-star far fa-star"></i>
                        </span>
                    </span>
                </div>
                <p>{{ list[activeIndex].overview }}</p>
                <div class="actions">
                    <button class="btn play">
                        <i class="fas fa-play"></i>
                    </button>
                    <button class="btn more">
                        <i class="fas fa-ellipsis-h"></i>
                    </button>
                </div>
            </div>
        </div>
        <CardList
            sectionTitle="Trends of the week"
            type="movie"
            v-if="list"
            :list="list"
        />
    </section>
</template>

<script>
import CardList from '@/components/CardList.vue'
export default {
    name: 'Hero',
    components: {
        CardList,
    },
    data() {
        return {
            activeIndex: 0,
            autoplayID: 0,
            stopSlider: false,
        }
    },
    props: {
        list: Array,
    },
    created() {
        this.autoPlay();
    },
    methods: {
        autoPlay() {
            this.stopSlider = false;
            this.autoplayID = setInterval(() => {
                this.activeIndex++;
                if(this.activeIndex === this.list.length - 1) {
                    this.activeIndex = 0
                }
            }, 4000)
        },
        stopAutoPlay() {
            clearInterval(this.autoplayID);
            this.stopSlider = true
        }
    }
}
</script>

<style scoped lang="scss">
.hero {
    padding-top: 70px;
    .trend {
        position: relative;
        img {
            width: 100%;
            max-height: 70vh;
            display: block;
            object-fit: cover;
            object-position: 100% 30%;
        }
        .trend-informations {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            min-height: 40%;
            overflow: auto;
            padding: 20px 30px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            background-color: rgba(33, 37, 41, 0.5);
            z-index: 1;
            h2 {
                text-transform: uppercase;
            }
            .language-votes {
                margin: 20px 0;
                strong {
                    color: rgb(220, 26, 40);
                }
                & .votes .star {
                    color: rgb(220, 26, 40);
                }
                & > span {
                    margin: 30px 50px;
                }
            }
            .actions {
                margin-top: 10px;
                align-self: end;
                .btn {
                    margin-right: 20px;
                    font-size: 30px;
                    color: rgb(220, 26, 40);
                    background-color: transparent;
                    border: none;
                    outline: none;
                    & > i {
                        padding: 10px;
                        border-radius: 50%;
                        border: 5px solid currentColor;
                    }
                    &.more > i {
                        border: none;
                    }
                    &:hover {
                        color: rgba(220, 26, 40, 0.8);
                        transform: scale(1.2);
                        cursor: pointer;
                    }
                }
            }
        }

    }
}
</style>