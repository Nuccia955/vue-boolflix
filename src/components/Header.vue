<template>
    <header>
        <input 
            type="text" 
            placeholder="Search movie or series"
            v-model="searchInput"
        >
        <button 
            @click="search"
        >
            Search
        </button>
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

</style>