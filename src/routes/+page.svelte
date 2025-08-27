<script>
    import Accordion from "$lib/Accordion.svelte";
    import { ArrowElbowRight, Envelope, InstagramLogo, LinkedinLogo } from "phosphor-svelte";
</script>

<div class="flex flex-col items-center justify-center min-h-screen text-center">
    <!-- Logo -->
    <img src="logo.svg" alt="Logo" class="w-3/13 mb-6" />

    <!-- Subtitel -->
    <h2 class="text-m font-light mb-4 text-gray-400">Geovisualisatie • GIS-oplossingen • Interactieve media</h2>

    <!-- Social links -->
    <div class="flex gap-6 mb-10 mt-8">
        <p class="text-m font-light mb-4">
            <ArrowElbowRight class="inline size-6 mr-2" />
            Snel naar: </p>
        <a href="https://www.linkedin.com/company/de-geomaten/?viewAsMember=true" target="_blank" class="text-blue-600 hover:underline">
            <LinkedinLogo class="size-6"></LinkedinLogo>
        </a>
        <a href="http://instagram.com/degeomaten/" target="_blank" class="text-pink-500 hover:underline">
            <InstagramLogo class="size-6"></InstagramLogo>
        </a>
        <a href="mailto:contact@degeomaten.nl" target="_blank" class="text-green-500 hover:underline">
            <Envelope class="size-6"></Envelope>
        </a>
    </div>

    <!-- Accordion -->
    <Accordion />
</div>

<style>
    * {
        font-family: "Inter" !important;
    }
</style>