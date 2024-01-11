<script >

export default {
    name: "AppCard",
    props: {
        result: Object
    },




    methods: {

        getImageUrl(posterPath) {
            if (posterPath) {
                // Aggiungi l'URL base per le immagini di TMDB e la dimensione desiderata
                const baseUrl = "https://image.tmdb.org/t/p/";
                const imageSize = "w342"; // Puoi modificare la dimensione secondo le tue esigenze
                return `${baseUrl}${imageSize}/${posterPath}`;
            } else {
                // Restituisci un'immagine di fallback o un messaggio se l'URL della copertina non è disponibile
                return "https://via.placeholder.com/150"; // Sostituisci con l'URL di un'immagine di fallback
            }
        },

        getLanguageFlag(languageCode) {

            let flagPath = `/${languageCode}.svg`;
            console
            // console.log(languageCode, flagPath);

            return flagPath;
        },

        convertToStars(voteAverage) {
            // Trasforma il voto da 1 a 10 in un numero intero da 1 a 5
            const convertedRating = Math.round(voteAverage / 2);

            return convertedRating

        }
    }

}

</script>

<template>
    <div class="app-card">
        <h2>{{ result.title || result.name }}</h2>

        <img :src="getImageUrl(result.poster_path)" :alt="result.title || result.name" />

        <p><strong>Titolo Originale:</strong> {{ result.original_title || result.original_name }}
        </p>
        <p><strong>Lingua:</strong> <img :src="getLanguageFlag(result.original_language)" class="flag"
                :alt="result.original_language">
        </p>
        <p><strong>Voto:</strong>
            <i class="fa-solid fa-star"></i>
            <FontAwesomeIcon icon="fas fa-coffee" />
            {{ convertToStars(result.vote_average) }}
        </p>
    </div>
</template>

<style scoped>
.flag {
    width: 15px;
}
</style>