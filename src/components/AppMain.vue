<script >

import AppCard from './AppCard.vue';

export default {
    name: "AppMain",

    components: {
        AppCard,
    },

    props: {
        searchResults: Array,
    },

};

</script>

<template>
    <main>
        <div>
            <h1>Risultati della ricerca:</h1>
            <div v-if="searchResults.length > 0" class="search-results">
                <div v-for="result in searchResults" :key="result.id" class="result-item">
                    <AppCard :result="result" />
                </div>

            </div>
            <div v-else>
                <div>Nessun risultato trovato</div>
            </div>
        </div>
    </main>
</template>

<style scoped></style>
