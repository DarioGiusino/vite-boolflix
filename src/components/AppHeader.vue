<script>
import SearchBar from './SearchBar.vue';
export default {
    name: 'App Header',
    components: { SearchBar }
}
</script>

<template>
    <header>
        <div class="container d-flex justify-content-between">
            <h1 class="text-uppercase">boolflix</h1>
            <search-bar></search-bar>
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