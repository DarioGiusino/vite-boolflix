<script>
import SearchBar from './SearchBar.vue';
export default {
    name: 'App Header',
    components: { SearchBar },
    emits: ['search-programs', 'writing-word']
}
</script>

<template>
    <header>
        <div class="container d-flex justify-content-between align-items-center">
            <!-- header title -->
            <h1 class="text-uppercase mb-0">boolflix</h1>

            <!-- searchbar -->
            <search-bar placeholder="Cerca film o serie TV" @form-submit="$emit('search-programs')"
                @writing="$emit('writing-word', $event)"></search-bar>
        </div>
    </header>
</template>

<style scoped lang="scss">
@use '../assets/scss/partials/variables.scss' as *;

header {
    background-color: $bg-black;
    color: $text-red;
    padding: 1rem;
}
</style>