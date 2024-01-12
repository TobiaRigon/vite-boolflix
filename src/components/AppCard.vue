<script >
import axios from 'axios';
import { store } from '../store';

export default {
    name: "AppCard",

    props: {
        result: Object
    },



    data() {
        return {
            store,
            cast: [],
            hasDetailsLoaded: false,
        };
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
                return "https://via.placeholder.com/342x513"; // Sostituisci con l'URL di un'immagine di fallback
            }
        },

        getLanguageFlag(languageCode) {

            let flagPath = `/${languageCode}.svg`;
            console
            // console.log(languageCode, flagPath);

            return flagPath;
        },

        convertToStars(voteAverage) {
            const convertedRating = Math.round(voteAverage / 2);

            // Utilizza FontAwesome per generare le icone stella in base al voto
            let starsHtml = "";
            for (let i = 0; i < 5; i++) {
                if (i < convertedRating) {
                    starsHtml += '<i class="fas fa-star" style="color: #FFD43B;"></i>';
                } else {
                    starsHtml += '<i class="far fa-star" style="color: #1f1f1f;"></i>';
                }
            }

            return starsHtml;
        },


        async fetchCast() {

            // Verifica se il risultato è una serie TV (utilizzando la proprietà 'first_air_date')
            if ('first_air_date' in this.result) {
                // Fai la richiesta all'API solo per le serie TV
                try {
                    const response = await axios.get(
                        `https://api.themoviedb.org/3/tv/${this.result.id}/season/1/aggregate_credits${store.apiKey}`
                    );

                    // Estrai solo i primi 5 membri del cast
                    this.cast = response.data.cast.slice(0, 5).map((member) => member.name);

                    // Imposta hasDetailsLoaded su true per mostrare i dettagli solo se sono stati caricati
                    this.hasDetailsLoaded = true;
                } catch (error) {
                    console.error("Errore durante il recupero del cast e dei generi:", error);
                }
            } else {
                try {
                    const response = await axios.get(
                        `https://api.themoviedb.org/3/movie/${this.result.id}/credits${store.apiKey}`
                    );

                    // Estrai solo i primi 5 membri del cast
                    this.cast = response.data.cast.slice(0, 5).map((member) => member.name);

                    // Imposta hasDetailsLoaded su true per mostrare i dettagli solo se sono stati caricati
                    this.hasDetailsLoaded = true;
                } catch (error) {
                    console.error("Errore durante il recupero del cast e dei generi:", error);
                }
            }
        },




        // Altri metodi esistenti
    },


};




</script>

<template>
    <div class="app-card" @mouseover="fetchCast">

        <img :src="getImageUrl(result.poster_path)" :alt="result.title || result.name" />


        <div class="details-overlay">
            <h2>{{ result.title || result.name }}</h2>
            <p><strong>Titolo Originale:</strong> {{ result.original_title || result.original_name }}</p>
            <p><strong>Lingua:</strong> <img :src="getLanguageFlag(result.original_language)" class="flag"
                    :alt="result.original_language"></p>
            <p><strong>Voto:</strong><span v-html="convertToStars(result.vote_average)"></span></p>
            <p><strong>Overview:</strong> {{ result.overview }}</p>
            <p v-if="hasDetailsLoaded && cast.length > 0"><strong>Cast:</strong> {{ cast.join(', ') }}</p>
        </div>


    </div>
</template>

<style scoped lang="scss">
.app-card {
    display: flex;
    align-items: center;
    position: relative;
    perspective: 1000px;
    transition: transform 0.8s;
    max-width: 388px;
    min-height: 576.5px;
    max-height: 663px;
    // margin: 15px 0;
    padding: 30px 21px;
    background-color: black;
    color: white;
    filter: drop-shadow(0px 3px 4px #000000);


    h2,
    p {
        padding-bottom: 15px;


    }


    .fa-star {
        color: yellow;
    }



    .flag {
        width: 15px;
    }

}

.card-front {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.app-card:hover {
    transform: rotateY(180deg);
}

.details-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0);
    color: white;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.0s ease 0.20s;
    transform: 0.8s;

    transform: rotateY(0deg) scale(-1, 1);
}

.app-card:hover .details-overlay {
    opacity: 1;

    transform-origin: center;
    transition: opacity 0.0s ease 0.20s;
    transform: 0.8s;

}

app-card:hover {
    transform: rotateY(0deg) scale(-1, 1);
}
</style>