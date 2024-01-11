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
            <div v-else class="new_search">
                <div>Fai una ricerca...</div>
            </div>
        </div>
    </main>
</template>

<style lang="scss" scoped>
main {
    height: calc(100vh - 80px);
    overflow-y: auto;
    padding-top: 15px;


    .search-results {
        margin: 0 auto;
        width: 85%;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;



    }

    .new_search {
        color: white;
        margin-left: 40px;
        font-size: 24px;
    }
}
</style>
