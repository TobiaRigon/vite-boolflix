<script >

export default {
    name: "AppCard",
    props: {
        result: Object
    },

}

</script>

<template>
    <div class="app-card">
        <h2>{{ result.title }}</h2>
        <p><strong>Titolo Originale:</strong> {{ result.original_title }}</p>
        <p><strong>Lingua:</strong> {{ result.original_language }}</p>
        <p><strong>Voto:</strong> {{ result.vote_average }}</p>
    </div>
</template>

<style scoped></style>
