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
        <h1 class="text-center">Films:</h1>
        <div class="d-flex flex-wrap">
            <programs-card v-for="movie in store.moviesList" v-bind="movie" :bannerUri="imgUri"
                bannerDefault="../assets/img/fallback_image.jpg"></programs-card>
        </div>

        <h1 class="text-center">Series:</h1>
        <div class="d-flex flex-wrap">
            <programs-card v-for="show in store.showsList" v-bind="show"></programs-card>
        </div>
    </main>
</template>

<style scoped>

</style>