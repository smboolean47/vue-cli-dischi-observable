<template>
    <div id="app">
        <Header/>

        <Main/>
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
    }
};
</script>

<style lang="scss">
@import "./assets/styles/general";
</style>
