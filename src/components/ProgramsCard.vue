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
            const url = new URL(`./assets/img/flags/${lang}.png`, import.meta.url);
            return url.href;
        },

    }
}
</script>

<template>
    <div class="program-card mb-4">

        <!-- <ul>
            <h1>----------------FILM---------------</h1>
            <li v-for="movie in store.moviesList" :key="movie.id">
                <span v-if="!movie.bannerUrl">-No banner-</span>
                <img v-else :src="`${imgUri}${movie.bannerUrl}`" alt="">

                {{ movie.title }},

                {{ movie.originalTitle }},

                <span>lang: </span>
                <figure v-if="movie.language == 'it' || movie.language == 'en'">
                    <img :src="renderFlag(movie.language)" alt="">,
                </figure>

                <span v-else>{{ movie.language }}</span>

                <p>{{ movie.desc || 'No description' }}</p>,

                {{ movie.rating }}
            </li>
            <br>
            <hr>
            <br>
            <h1>----------------SERIES---------------</h1>
            <li v-for="show in store.showsList" :key="show.id">
                <span v-if="!show.bannerUrl">-No banner-</span>
                <img v-else :src="`${imgUri}${show.bannerUrl}`" alt="">

                {{ show.title }},

                {{ show.originalTitle }},

                <span>lang: {{ show.language }}</span>

                <figure v-if="show.language == 'it' || show.language == 'en'">
                    <img :src="renderFlag(show.language)" alt="">,
                </figure>

                <p>{{ show.desc || 'No description' }}</p>,

                {{ show.rating }}
            </li>
        </ul> -->
        <img v-if="bannerUrl" :src="`${bannerUri}${bannerUrl}`" :alt="title">
        <img v-else src="../assets/img/fallback_image.jpg" :alt="title">

        <div class="program-info">
            <h1 class="mb-0">{{ title }}</h1>
            <em class="d-block mb-2">-{{ originalTitle }}-</em>
            <p>lingua: {{ language }}</p>
            <p>voto: {{ rating }}</p>
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

h1 {
    font-size: 40px;
}

em {
    font-size: 12px;
}
</style>