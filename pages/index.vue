<template>
<div class="bg-black text-white font-helN">
    <site-header />

    <div class="h-screen w-screen z-0 overflow-hidden relative">
        <img v-bind:src="hero.bg" class="absolute w-screen left-0 z-0" alt="" />
        <gradient />
        <div class="absolute z-50 w-screen flex justify-center bottom-0">
            <div class="container pb-16">
                <div v-html="hero.tagline" class="tagline container mx-auto text-white font-helN text-6xl" />
                <div class="tagline text-white font-prox text-6xl -mt-12"><span>...</span></div>
            </div>
        </div>
    </div>

    <bio />
</div>
</template>

<script>
import SiteHeader from "~/components/SiteHeader.vue";
import Gradient from "~/components/home/Gradient.vue";
import Bio from "~/components/home/Bio.vue";

export default {
    components: {
        SiteHeader,
        Gradient,
        Bio,
    },

    mounted() {
        fetch(`${process.env.get_singletons}/home`, {
                headers: {
                    "Cockpit-Token": process.env.token,
                },
            })
            .then((response) => response.json())
            .then((result) => {
                this.hero.bg = process.env.cockpit + result.hero.bg.path;
                this.hero.tagline = result.hero.tagline;
            });
    },

    data: function () {
        return {
            hero: {
                bg: "",
                tagline: "",
            },
        };
    },
};
</script>

<style>
.tagline em {
    font-style: normal;
    color: var(--color-pri);
}
</style>
