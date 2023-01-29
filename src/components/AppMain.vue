<script>
import ProgramsCard from './ProgramsCard.vue';
import { store } from '../data/store';
import { imgUri } from '../data';
export default {
    name: 'App Main',
    components: { ProgramsCard },

    data() {
        return {
            store,
            imgUri
        }
    }
}
</script>

<template>
    <main class="container p-5">
        <div v-if="!store.moviesList.length && !store.showsList.length">
            <!-- ? default text if search is not done -->
            <h1>Cerca un programma dalla barra in alto...</h1>
        </div>

        <div v-else>
            <!-- ? movies cards -->
            <h1 class="text-center">Films:</h1>
            <div class="d-flex flex-wrap">
                <programs-card v-for="movie in store.moviesList" v-bind="movie" :bannerUri="imgUri"></programs-card>
            </div>

            <!-- ? series cards -->
            <h1 class="text-center mt-5">Series:</h1>
            <div class="d-flex flex-wrap">
                <programs-card v-for="show in store.showsList" v-bind="show" :bannerUri="imgUri"></programs-card>
            </div>
        </div>
    </main>
</template>

<style scoped>

</style>