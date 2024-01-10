<script >

export default {
    name: "AppMain",
    props: {
        searchResults: Array, // Proprietà per ricevere i risultati della ricerca da AppHeader
    },

};

</script>

<template>
    <main>
        <div>
            <h1>Risultati della ricerca:</h1>
            <div v-if="searchResults && searchResults.length > 0" class="search-results">
                <div v-for="result in searchResults" :key="result.id" class="result-item">
                    <h2>{{ result.title || result.name }}</h2>
                    <p>Titolo Originale: {{ result.original_title || result.original_name }}</p>
                    <p>Lingua: {{ result.original_language }}</p>
                    <p>Voto: {{ result.vote_average }}</p>
                    <!-- Aggiungi altre informazioni desiderate -->
                </div>
            </div>
            <div v-else>
                <p>Nessun risultato trovato</p>
            </div>
        </div>
    </main>
</template>

<style scoped></style>
