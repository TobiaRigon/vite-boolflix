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
                <AppCard />
            </div>
            <div v-else>
                <div>Nessun risultato trovato</div>
            </div>
        </div>
    </main>
</template>

<style scoped></style>
