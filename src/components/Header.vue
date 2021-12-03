<template>
    <header>
        <div class="logo"
            @click="getTrendsOfTheWeek">
            <img src="https://fontmeme.com/permalink/211201/4937b74c6317b36c509baa13669b4b20.png" alt="logo">
        </div>
        <nav>
            <ul class="links">
                <li>
                    <a @click.prevent="getTrendsOfTheWeek">Home</a>
                </li>
                <li>
                    <a @click.prevent="getTrendsOfTheWeek">Trends of the week</a>
                </li>
                <li>
                    <a>Log in</a>
                </li>
            </ul>
            <div class="searchbar">
                <input class="search"
                    type="text" 
                    placeholder="Search movie or series"
                    v-model="searchInput"
                    @keyup.enter="search"
                >
                <button class="btn-search"
                    @click="search"
                >
                    Search
                </button>
            </div>
        </nav>
    </header>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {
            searchInput: '',
        }
    },
    methods: {
        search() {
            this.$emit('performSearch', this.searchInput)
        },
        getTrendsOfTheWeek() {
            this.searchInput = '';
            this.$emit('performTrendsOfTheWeek')
        }
    }
}
</script>

<style scoped lang="scss">
header {
    width: 100%;
    height: 75px;
    position: fixed;
    top: 0;
    z-index: 2;
    background-color: #1e2125;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .logo {
        cursor: pointer;
        margin: 10px 50px;
        max-width: 150px;
        img {
            width: 100%;
        }
    }
    nav {
        display: flex;
        align-items: center;
        ul.links {
            list-style: none;
            display: flex;
            align-items: center;
            margin-right: 20px;
            li {
                margin-right: 20px;
                a {
                    cursor: pointer;
                    line-height: 75px;
                    font-size: 1.1em;
                    display: inline-block;
                    &:hover {
                        color: rgb(220, 26, 40);
                    }
                    &:active {
                        color: rgba(220, 26, 40, 0.8);
                    }
                }
            }            
        }
        .searchbar {
            input.search {
                width: 200px;
                padding: 3px 15px;
                margin-right: 15px;
            }
            .btn-search {
                padding: 5px 20px;
                font-size: 0.8rem;
                border-radius: 15px;
                color: white;
                background-color: rgb(220, 26, 40);
                border: none;
                outline: none;
                cursor: pointer;

                &:hover {
                    background-color: rgba(220, 26, 40, 0.8);
                }
                &:active {
                    transform: scale(1.1);
                }
            }
        }
    }

}

</style>