<script lang="ts">
  import { onMount, onDestroy, setContext, untrack } from "svelte";
  import MapLibreGL from "maplibre-gl";
  import "maplibre-gl/dist/maplibre-gl.css";
  import { browser } from "$app/environment";

  let tailwindTheme: "light" | "dark" = $state("light");

  type MapStyleOption = string | MapLibreGL.StyleSpecification;

  interface Props {
    children?: import("svelte").Snippet;
    styles?: {
      light?: MapStyleOption;
      dark?: MapStyleOption;
    };
    theme?: "light" | "dark";
    center?: [number, number];
    zoom?: number;
    options?: Omit<MapLibreGL.MapOptions, "container" | "style">;
    scrollY?: number;
  }

  const defaultStyles = {
    dark: "https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json",
    light: "https://basemaps.cartocdn.com/gl/positron-gl-style/style.json",
  };

  let {
    children,
    styles,
    theme: _theme = "light",
    center = [13.405, 52.52],
    zoom = 11,
    options = {},
    scrollY,
  }: Props = $props();

  let mapContainer: HTMLDivElement;
  let map: MapLibreGL.Map | null = $state(null);
  let isMounted = $state(false);
  let isLoaded = $state(false);
  let isStyleLoaded = $state(false);
  let initialStyleApplied = false;

  const mapStyles = $derived({
    dark: styles?.dark ?? defaultStyles.dark,
    light: styles?.light ?? defaultStyles.light,
  });

  const currentStyle = $derived(
    tailwindTheme === "dark" ? mapStyles.dark : mapStyles.light,
  );

  const isReady = $derived(isMounted && isLoaded && isStyleLoaded);

  setContext("map", {
    getMap: () => map,
    isLoaded: () => isReady,
  });

  $effect(() => {
    const scrollOffset = scrollY ?? 0;
    if (!map) return;

    const center = map.getCenter();
    const zoom = map.getZoom();

    map.setPitch(scrollOffset / 10);
  });

  onMount(() => {
    isMounted = true;

    if (browser) {
      const root = document.documentElement;

      const updateTheme = () => {
        tailwindTheme = root.classList.contains("dark") ? "dark" : "light";
      };

      updateTheme();

      const observer = new MutationObserver(updateTheme);
      observer.observe(root, {
        attributes: true,
        attributeFilter: ["class"],
      });

      onDestroy(() => observer.disconnect());
    }

    const mapInstance = new MapLibreGL.Map({
      container: mapContainer,
      style: currentStyle,
      center,
      zoom,
      minZoom: 6,
      maxZoom: 16,
      attributionControl: false,
      ...options,
    });

    // setTimeout(() => {
    //   mapInstance.flyTo({ center, zoom, pitch: 45 });
    // }, 500);

    mapInstance.on("load", () => {
      isLoaded = true;

      //   mapInstance.addLayer({
      //     id: "green-tint",
      //     type: "background",
      //     paint: {
      //       "background-color": "rgba(30, 180, 50, 0.25)",
      //     },
      //   });

      const style = mapInstance.getStyle();
      const layers = style.layers;

      const WATER_COLOR = "rgba(210, 210, 210, 1)";
      mapInstance.setPaintProperty("background", "background-color", "#91C07E");
      mapInstance.setPaintProperty("landcover", "fill-color", "#00BA77");
      mapInstance.setPaintProperty(
        "park_national_park",
        "fill-color",
        "#00BA77",
      );
      mapInstance.setPaintProperty(
        "park_nature_reserve",
        "fill-color",
        "#00BA77",
      );
      mapInstance.setPaintProperty(
        "landuse_residential",
        "fill-color",
        "#9AC384",
      );
      mapInstance.setPaintProperty("landuse", "fill-color", "#87BE84");
      mapInstance.setPaintProperty("waterway", "line-color", "#255E17");
      mapInstance.setPaintProperty("water", "fill-color", "#008E00");
      mapInstance.setPaintProperty("water_shadow", "fill-color", "#255E17");
      mapInstance.setPaintProperty("building", "fill-color", "#DFDBBF");
      mapInstance.setPaintProperty("building-top", "fill-color", "#DFDBBF");
      mapInstance.setPaintProperty("boundary_state", "line-color", "#255E17");
      mapInstance.setPaintProperty("boundary_county", "line-color", "#00f");
      mapInstance.setPaintProperty(
        "boundary_country_inner",
        "line-color",
        "#255E17",
      );
      mapInstance.setPaintProperty("boundary_country_inner", "line-width", 2);
      mapInstance.setPaintProperty(
        "boundary_country_outline",
        "line-color",
        "#00000000",
      );
      mapInstance.setPaintProperty(
        "road_trunk_fill_noramp",
        "line-color",
        "#f00",
      );
      mapInstance.setPaintProperty(
        "road_mot_fill_noramp",
        "line-color",
        "#f00",
      );

      console.log(layers);
      layers.forEach((layer) => {
        // if (
        //   layer.id.includes("label") ||
        //   layer.id.includes("place") ||
        //   layer.id.includes("name")
        // ) {
        //   mapInstance.setLayoutProperty(layer.id, "visibility", "none");
        // }
        if (layer.id.includes("road")) {
          const paint = mapInstance.getLayer(layer.id)?.type === "line";
          if (paint) {
            mapInstance.setPaintProperty(layer.id, "line-color", "#DFDBBF");
          }
        }
      });
    });

    mapInstance.on("styledata", () => {
      isStyleLoaded = true;
      initialStyleApplied = true;
    });

    map = mapInstance;
  });

  $effect(() => {
    const style = currentStyle;

    if (!map || !initialStyleApplied) {
      return;
    }

    untrack(() => {
      isStyleLoaded = false;
      map!.setStyle(style, { diff: true });
    });
  });

  $effect(() => {
    if (!map || !isReady) {
      return;
    }

    const [lng, lat] = center;

    untrack(() => {
      map!.easeTo({ center: [lng, lat], zoom });
    });
  });

  onDestroy(() => {
    map?.remove();
    map = null;
    isLoaded = false;
    isStyleLoaded = false;
  });
</script>

<div bind:this={mapContainer} class="relative h-full w-full">
  {#if !isReady}
    <div class="absolute inset-0 flex items-center justify-center">
      <div class="flex gap-1">
        <span class="bg-muted-foreground/60 size-1.5 animate-pulse rounded-full"
        ></span>
        <span
          class="bg-muted-foreground/60 size-1.5 animate-pulse rounded-full [animation-delay:150ms]"
        ></span>
        <span
          class="bg-muted-foreground/60 size-1.5 animate-pulse rounded-full [animation-delay:300ms]"
        ></span>
      </div>
    </div>
  {/if}
  {#if isReady}
    {@render children?.()}
  {/if}
</div>
