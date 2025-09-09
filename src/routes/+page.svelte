<script>
    // import { onMount } from 'svelte';
    import Accordion from "$lib/Accordion.svelte";
    import { ArrowElbowRight, Envelope, InstagramLogo, LinkedinLogo } from "phosphor-svelte";

    // let mounted = false;
    // onMount(() => { mounted = true });
</script>

<div class="flex flex-col items-center justify-center min-h-screen px-4 sm:px-6 lg:px-8 text-center">
    <!-- Logo -->
    <img src="logo.svg" alt="Logo" class="w-72 sm:w-72 md:w-72 mb-6" />

    <!-- Subtitel -->
    <h2 class="text-sm sm:text-base md:text-base font-light mb-4 text-gray-400">
        Geovisualisatie • GIS-oplossingen • Interactieve media
    </h2>

    <!-- Social links -->
    <div class="flex flex-wrap justify-center gap-4 sm:gap-6 mb-10 mt-6">
        <p class="text-sm sm:text-base font-light flex items-center gap-1 mb-2 sm:mb-0">
            <ArrowElbowRight class="inline size-5 sm:size-6" />
            Snel naar:
        </p>
        <a href="https://www.linkedin.com/company/de-geomaten/?viewAsMember=true" target="_blank" class="text-blue-600 hover:underline">
            <LinkedinLogo class="size-5 sm:size-6"></LinkedinLogo>
        </a>
        <a href="http://instagram.com/degeomaten/" target="_blank" class="text-pink-500 hover:underline">
            <InstagramLogo class="size-5 sm:size-6"></InstagramLogo>
        </a>
        <a href="mailto:contact@degeomaten.nl" target="_blank" class="text-green-500 hover:underline">
            <Envelope class="size-5 sm:size-6"></Envelope>
        </a>
    </div>

    <!-- {#if mounted} -->
        <Accordion />
    <!-- {/if} -->
</div>

<style>
    * {
        font-family: "Inter" !important;
    }
</style>