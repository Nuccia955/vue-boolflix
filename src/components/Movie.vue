<template>
    <li class="movie">
        <ul>
            <li>Titolo</li>
            <li>Titolo Originale</li>
            <li>Lingua</li>
            <li>Voto</li>
        </ul>
    </li>
</template>

<script>
export default {
    name: 'Movie',
}
</script>

<style scoped lang="scss">
li.movie {
    margin: 50px 0;
    ul {
        list-style: disc;
    }
}
</style>