<script lang="ts">
  import PowerWidget from '$lib/components/PowerWidget.svelte';
</script>

<svelte:head>
  <title>Power App</title>
  <meta name="description" content="Test application for power widget">
</svelte:head>

<PowerWidget />

<style>
  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>