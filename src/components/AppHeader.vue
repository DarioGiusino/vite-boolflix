<script>
import SearchBar from './SearchBar.vue';
export default {
    name: 'App Header',
    components: { SearchBar }
}
</script>

<template>
    <header>
        <div class="container d-flex justify-content-between align-items-center">
            <h1 class="text-uppercase">boolflix</h1>
            <search-bar placeholder="Cerca film o serie TV"></search-bar>
        </div>
    </header>
</template>

<style scoped lang="scss">
@use '../assets/scss/style.scss' as *;

header {
    background-color: $bg-black;
    color: $text-red;
}
</style>