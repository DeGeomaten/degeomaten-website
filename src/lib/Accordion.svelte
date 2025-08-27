<script lang="ts">
  import { Accordion } from "bits-ui";
  import CaretDown from "phosphor-svelte/lib/CaretDown";
 
  const items = [
    {
      value: "1",
      title: "Wie zijn 'De Geomaten'?",
      content: "Wij zijn <b>Gees</b> en <b>Josephine</b>. Tijdens onze master Geomatics aan de TU Delft ontdekten we hoe goed onze verschillende achtergronden elkaar aanvullen – Gees met Computer Science and Engineering, Josephine met Bouwkunde. Samen delen we een nieuwsgierigheid naar hoe data en ruimte elkaar beïnvloeden, en hoe je dat zichtbaar kunt maken met kaarten en visualisaties."
    },
    {
      value: "2",
      title: "Wat doen de Geomaten?",
      content: "De Geomaten vertalen ruimtelijke data naar duidelijke kaarten en interactieve toepassingen. We maken complexe informatie begrijpelijk en aantrekkelijk, zodat organisaties en onderzoekers sneller inzichten krijgen en beter kunnen vertellen wat hun data betekent. Of het nu gaat om een klein GIS-klusje of een creatieve visualisatie: wij zetten onze kennis en energie graag in om ruimtelijke verhalen tot leven te brengen."
    }
  ];
</script>

<Accordion.Root class="w-[500px] sm:max-w-[70%]" type="multiple">
  {#each items as item (item.value)}
    <Accordion.Item
      value={item.value}
      class="border-dark-10 group border-b px-1.5"
    >
      <Accordion.Header>
        <Accordion.Trigger
          class="flex w-full flex-1 select-none items-center justify-between py-5 text-[15px] font-medium transition-all [&[data-state=open]>span>svg]:rotate-180"
        >
          <span class="w-full text-left">
            {item.title}
          </span>
          <span
            class="hover:bg-dark-10 inline-flex size-8 items-center justify-center rounded-[7px] bg-transparent"
          >
            <CaretDown class="size-[18px] transition-transform duration-200" />
          </span>
        </Accordion.Trigger>
      </Accordion.Header>
      <Accordion.Content
        class="data-[state=closed]:animate-accordion-up data-[state=open]:animate-accordion-down overflow-hidden text-sm tracking-[-0.01em]"
      >
        <div class="pb-[25px]">
          {@html item.content}
        </div>
      </Accordion.Content>
    </Accordion.Item>
  {/each}
</Accordion.Root>