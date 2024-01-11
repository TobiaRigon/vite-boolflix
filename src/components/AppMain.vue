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

<style lang="scss" scoped>
main {
    height: calc(100vh - 80px);
    overflow-y: auto;
    padding-top: 40px;

    .search-results {
        margin: 0 auto;
        width: 85%;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;



    }
}
</style>
