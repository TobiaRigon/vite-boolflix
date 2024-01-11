<script >

export default {
    name: "AppCard",
    props: {
        result: Object
    },



    methods: {
        getLanguageFlag(languageCode) {

            let flagPath = `../assets/flags/${languageCode}.svg`;
            console
            console.log(languageCode, flagPath);

            return flagPath;
        }
    }

}

</script>

<template>
    <div class="app-card">
        <h2>{{ result.title }}</h2>
        <p><strong>Titolo Originale:</strong> {{ result.original_title || result.original_name }}
        </p>
        <p><strong>Lingua:</strong> <img :src="getLanguageFlag(result.original_language)" :alt="result.original_language">
        </p>
        <p><strong>Voto:</strong> {{ result.vote_average }}</p>
    </div>
</template>

<style scoped>
img {
    width: 13px;
}
</style>
