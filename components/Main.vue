<template>
    <main class="container mt-5">
        <div class="d-flex flex-wrap">
            <Disc
                v-for="(discItem, index) in filteredDiscs"
                :key="index"
                :disc="discItem"
            />
        </div>
    </main>
</template>

<script>
import axios from "axios";
import Disc from "./Disc";

export default {
    name: "Main",
    components: {
        Disc,
    },
    props: {
        selectedGenre: String,
    },
    computed: {
        // questa computed si attiva tutte le volte che cambia genreToSearch
        // se la stringa del genere da cercare è vuota restituisco tutta la lista
        // arimenti la giltro in base al genere
        filteredDiscs() {
            if (this.selectedGenre === "") {
                return this.discs;
            }
            return this.discs.filter(
                (item) => item.genre === this.selectedGenre
            );
        },
    },
    data() {
        return {
            discs: [],
            genres: [],
        };
    },
    created() {
        axios
            .get("https://flynn.boolean.careers/exercises/api/array/music")
            .then((res) => {
                this.discs = res.data.response;

                // inizialmente inseriamo nella select i generi in modo statico
                // poi facciamo vedere come popolare la select dinamicamente
                // recuperando i generi direttamente dall'array di dischi
                this.discs.forEach((disc) => {
                    if (!this.genres.includes(disc.genre)) {
                        this.genres.push(disc.genre);
                    }
                });
                // passo la lista dei generi, che servirà per la select, con un $emit
                this.$emit("genresReady", this.genres);
            })
            .catch((err) => {
                console.log(err);
            });
    },
};
</script>