<script lang="ts">
  import "./layout.css";

  let { children } = $props();
</script>

<svelte:head>
  <title>De Geomaten</title>
  <link rel="shortcut icon" href="/favicon.ico" type="image/x-icon" />
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
</svelte:head>
{@render children()}
