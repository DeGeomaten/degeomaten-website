<script lang="ts">
  import "./layout.css";
  import favicon1 from "$lib/assets/favicon-16x16.png";
  import favicon2 from "$lib/assets/favicon-32x32.png";
  import favicon3 from "$lib/assets/favicon.ico";
  import favicon4 from "$lib/assets/apple-touch-icon.png";

  let { children } = $props();
</script>

<svelte:head>
  <title>De Geomaten</title>
  <link rel="shortcut icon" href={favicon3} type="image/x-icon" />
  <link rel="icon" type="image/png" sizes="32x32" href={favicon2} />
  <link rel="icon" type="image/png" sizes="16x16" href={favicon1} />
  <link rel="apple-touch-icon" sizes="180x180" href={favicon4} />
</svelte:head>
{@render children()}
