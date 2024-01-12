<script >

import AppCard from './AppCard.vue';

export default {
    name: "AppMain",



    components: {
        AppCard,
    },

    props: {
        searchResults: Array,
        startSearchProp: Function,
        loading: Boolean,
    },

    methods: {
        eseguiStartSearch() {
            if (typeof this.startSearchProp === 'function') {
                this.startSearchProp();
            }
        },


    },
};

</script>

<template>
    <main>
        <div v-if="loading" class="loader"> <i class="fas fa-spinner fa-spin" style="color: white;"></i></div>
        <div v-else>
            <!-- Il blocco dei risultati o della nuova ricerca -->
            <div v-if="searchResults.length > 0" class="search-results">
                <div v-for="result in searchResults" :key="result.id" class="result-item">
                    <AppCard :result="result" />
                </div>
            </div>
            <div v-else class="new_search">
                <button @click="eseguiStartSearch">Mi sento fortunato!</button>
            </div>
        </div>
    </main>
</template>

<style lang="scss" scoped>
main {
    height: calc(100vh - 80px);
    overflow-y: auto;
    padding-top: 40px;


    .loader {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100%;

        .fa-spinner {
            font-size: 60px;
            margin-right: 10px;
        }

        .fa-spin {
            animation: spin 1s infinite linear;
        }


        @keyframes spin {
            from {
                transform: rotate(0deg);
            }

            to {
                transform: rotate(360deg);
            }
        }
    }

}





.search-results {
    margin: 0 auto;
    width: 90%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;



}

.new_search {
    color: white;
    margin-left: 40px;
    font-size: 24px;
}

button {

    margin: 20px auto;
    font-size: 25px;
    border: 0;
    padding: 5px;

}
</style>
