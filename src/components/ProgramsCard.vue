<script>
export default {
    name: 'Programs Card',
    props: {
        title: String,
        originalTitle: String,
        language: String,
        rating: Number,
        desc: String,
        bannerUrl: String,
        bannerUri: String,
    },

    methods: {
        //build the url for the flag image
        renderFlag(lang) {
            const url = new URL(`../assets/img/flags/${lang}.png`, import.meta.url);
            return url.href;
        },

    }
}
</script>

<template>
    <!-- # programs card -->
    <div class="program-card mb-4">
        <!-- ? banner image, if not existent show a default image -->
        <img v-if="bannerUrl" :src="`${bannerUri}${bannerUrl}`" :alt="title">
        <img v-else src="../assets/img/fallback_image.jpg" :alt="title">

        <!-- ? :hover show program info -->
        <div class="program-info">
            <!-- title & original title -->
            <h1 class="mb-0">{{ title }}</h1>
            <em class="d-block mb-2">-{{ originalTitle }}-</em>

            <!-- show language flags as image or the language as text -->
            <figure v-if="language == 'it' || language == 'en'">
                <img :src="renderFlag(language)" :alt="language">
            </figure>
            <p v-else>lingua: {{ language }}</p>

            <!-- program rating -->
            <p>voto: {{ rating }}/5</p>

            <!-- program description -->
            <p><strong>Descrizione: </strong>{{ desc || "Nessuna descrizione trovata." }}</p>
        </div>
    </div>
</template>

<style scoped>
.program-card {
    width: 342px;
    min-height: 520px;
    overflow-y: auto;
    border-radius: 5px;
    margin: 0 20px;

    position: relative;
}

.program-card img {
    display: block;
    height: 100%;
    width: 100%;
}

.program-info {
    background-color: rgba(0, 0, 0, 0.8);
    height: 100%;
    padding: 1rem;
    text-align: center;

    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    z-index: -1;
    opacity: 0;
    overflow: auto;

    transition: opacity 0.65s, z-index 0.65s;
}

.program-card:hover .program-info {
    opacity: 1;
    z-index: 1;
}

.program-info figure {
    margin: 0 auto;
    margin-bottom: 1.25rem;
    width: 30px;
    height: 20px;
}

h1 {
    font-size: 40px;
}

em {
    font-size: 12px;
}
</style>