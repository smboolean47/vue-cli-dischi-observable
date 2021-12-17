<template>
    <div id="app">
        <Header :genres="genresList" @changedGenre="startSeach" />

        <Main :selectedGenre="genreToSearch" @genresReady="getGenresList" />
    </div>
</template>

<script>
import Header from "./components/Header";
import Main from "./components/Main";

export default {
    name: "App",
    components: {
        Header,
        Main,
    },
    data() {
        return {
            genresList: [],
            genreToSearch: "",
        };
    },
    methods: {
        getGenresList(allGenres) {
            this.genresList = allGenres;
        },
        startSeach(genreToSearch) {
            this.genreToSearch = genreToSearch;
        },
    },
};
</script>

<style lang="scss">
@import "./assets/styles/general";
</style>
