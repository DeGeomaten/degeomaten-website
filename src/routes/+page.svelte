<script lang="ts">
  import { Card } from "$lib/components/ui/card";
  import { Map, MapControls, MapPopup } from "$lib/components/ui/map";
  import Button from "$lib/components/ui/button/button.svelte";
  import LightSwitch from "$lib/components/ui/light-switch/light-switch.svelte";
  import { ModeWatcher, mode } from "mode-watcher";

  import { Mails } from "lucide-svelte";

  let showPopup = $state(true);
</script>

<!-- <ModeWatcher /> -->

<header
  class="relative h-50 bg-[linear-gradient(180deg,#A384FF22_0%,rgba(255,255,255,0.1)_100%)] flex justify-end p-2"
>
  <div class="absolute inset-0 flex flex-col items-center justify-center gap-1">
    <img src="logo.svg" alt="Logo" class="logo size-64" />
  </div>

  <!-- <div class="z-10">
    <LightSwitch />
  </div> -->
</header>

<section
  class="flex justify-center flex-col gap-4 mt-10 text-center px-4 w-[100%] sm:w-[75%] max-w-200 m-auto"
>
  <h1 class="text-2xl text-[#C99EFF]">Moderne Cartografie</h1>
  <h2 class="text-md text-[#6A0DAD]">
    Geovisualisatie • GIS-oplossingen • Interactieve media
  </h2>
  <p class="text-[#6A0DAD]">
    Wij vertalen ruimtelijke data naar heldere, visueel sterke kaarten en
    toepassingen. Met moderne cartografie, GIS en interactieve media maken we
    informatie toegankelijk en inzichtelijk.
  </p>
</section>

<!-- <div class="text-center mt-10">
  <Button class="bg-[#255E17] text-white hover:bg-[#A384FF] display">
    <Mails class="size-4 mr-2" />
    Neem contact op &rarr;</Button
  >
</div> -->

<Card class="relative w-[75%] max-w-200 h-100 m-auto mt-10 overflow-hidden p-0">
  <div
    class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,#ffffff00,#005E0066)] z-10 pointer-events-none"
  ></div>
  <Map center={[4.48, 51.92]} zoom={12}>
    <MapControls />
    {#if showPopup}
      <MapPopup
        longitude={4.462}
        latitude={51.909}
        closeButton
        focusAfterOpen={false}
        closeOnClick={false}
        onclose={() => (showPopup = false)}
        class="w-50"
      >
        <div class="space-y-2">
          <p class="text-[#6A0DAD] text-sm">
            <b class="underline">De Geomaten</b> is gevestigd in
            <b>Rotterdam</b>
          </p>
          <Button
            size="sm"
            variant="outline"
            class="w-full"
            onclick={() => (showPopup = false)}
          >
            Sluiten
          </Button>
        </div>
      </MapPopup>
    {/if}
  </Map>
</Card>

<section
  class="flex justify-center w-[100%] sm:w-[75%] max-w-200 m-auto flex-col gap-4 mt-10 text-center px-4"
>
  <h1 class="text-2xl text-[#C99EFF]">Recente projecten</h1>
  <p class="text-[#6A0DAD]">
    &rarr;
    <a href="https://watertijdreis.nl" class="underline font-bold"
      >Watertijdreis.nl</a
    > brengt 125 jaar Nederlandse watergeschiedenis in kaart, met 955 gedigitaliseerde
    kaartbladen (1865-1992). Gebruikers kunnen tijdreizen door de geschiedenis van
    waterbeheer.
  </p>
  <div class="flex gap-4 mt-[-40px] justify-center items-center flex-wrap">
    <img src="rce-logo.svg" class="size-32" alt="" />
    <img src="stowa-logo.svg" class="size-24" alt="" />
    <img src="tu-logo.svg" class="size-28" alt="" />
    <img src="allmaps-logo.svg" class="size-12" alt="" />
  </div>
  <p class="text-[#6A0DAD]">
    &rarr;
    <a href="https://talenkaart.nl/amsterdam" class="underline font-bold"
      >Talenkaart.nl</a
    >
    is een interactieve kaart die de meertaligheid van Amsterdam in beeld brengt.
    In samenwerking met taalwetenschapper Eva van Lier (UvA) visualiseren we welke
    talen in de stad worden gesproken en hoe meertaligheid de stad structureert.
    Geïnspireerd door The New York Times, biedt deze kaart inzicht in de taalkundige
    diversiteit per stadsdeel en helpt organisaties om inwoners beter te bereiken.
    <img
      src="logo-uva.png"
      alt="Logo Universiteit van Amsterdam"
      class="h-12 m-auto mt-4"
    />
  </p>
</section>

<section
  class="flex justify-center w-[100%] sm:w-[75%] max-w-200 m-auto flex-col gap-4 mt-10 text-center px-4 text-[#6A0DAD]"
>
  <h1 class="text-2xl text-[#C99EFF]">Samenwerken?</h1>

  <Button
    class="w-54 m-auto my-6 bg-[#6A0DAD] text-white hover:bg-[#A384FF] display"
    onclick={() => (window.location.href = "mailto:contact@degeomaten.nl")}
  >
    <Mails class="size-4 mr-2" />
    Stuur ons een mailtje &rarr;
  </Button>

  <p>
    Naar onze <a
      class="underline"
      href="https://www.linkedin.com/company/de-geomaten">LinkedIn-pagina</a
    >
    &rarr;
  </p>
  <p>
    Naar onze <a class="underline" href="https://www.instagram.com/degeomaten/"
      >Instagram-pagina</a
    >
    &rarr;
  </p>
</section>

<footer
  class="w-full h-50 bg-[#A384FF] mt-10 text-white flex flex-col items-center justify-center"
>
  <img src="logo.svg" class="size-42 invert" alt="" />
  <a class="underline" href="mailto:contact@degeomaten.nl"
    >contact@degeomaten.nl</a
  >
  <p class="my-4">De Geomaten &copy; 2026</p>
</footer>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&family=Gidugu&family=Young+Serif&display=swap");

  :global(img.logo) {
    filter: brightness(0) saturate(100%) invert(25%) sepia(100%) saturate(2000%)
      hue-rotate(240deg) brightness(90%) contrast(100%);
  }

  :global(*) {
    font-family: "Inter", sans-serif;
  }

  :global(h1, h2, h3) {
    font-family: "Young Serif", sans-serif;
  }
</style>
