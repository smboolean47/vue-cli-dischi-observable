<template>
    <main class="container mt-5">
        <div class="d-flex flex-wrap">
            <Disc v-for="(discItem, index) in filteredDiscs" :key="index" :disc="discItem"/>
        </div>
    </main>
</template>

<script>
import data from '../share/data';
import axios from "axios";
import Disc from "./Disc";

export default {
    name: "Main",
    components: {
        Disc,
    },
    computed: {
        filteredDiscs() {
            if (data.genreToSearch === "") {
                return this.discs;
            }
            return this.discs.filter(
                (item) => item.genre === data.genreToSearch
            );
        },
    },
    data() {
        return {
            data,
            discs: []
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
                    if (!data.genresList.includes(disc.genre)) {
                        data.genresList.push(disc.genre);
                    }
                });
            })
            .catch((err) => {
                console.log(err);
            });
    },
};
</script>