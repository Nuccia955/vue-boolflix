<template>
    <header>
        <div class="logo">
            <img src="https://fontmeme.com/permalink/211201/4937b74c6317b36c509baa13669b4b20.png" alt="logo">
        </div>
        <div class="searchbar">
            <input class="search"
                type="text" 
                placeholder="Search movie or series"
                v-model="searchInput"
            >
            <button class="btn-search"
                @click="search"
            >
                Search
            </button>
        </div>
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
    }
}
</script>

<style scoped lang="scss">
header {
    width: 100%;
    position: fixed;
    top: 0;
    z-index: 2;
    background-color: #1e2125;
    padding: 10px 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .logo {
        max-width: 150px;
        img {
            width: 100%;
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

</style>