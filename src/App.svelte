<script>
  import Chart from './components/Chart.svelte';
  import AccessibleChart from './components/AccessibleChart.svelte';
  import ReactiveDataStory from './components/ReactiveDataStory.svelte';
  import ReactiveStores from './components/ReactiveStores.svelte';
  import Mapping from './components/Mapping.svelte';

  let selectedComponent = 'Chart'; // Default selection

  // Components dictionary
  let components = {
    Chart,
    AccessibleChart,
    ReactiveDataStory,
    ReactiveStores,
    Mapping
  };

  // This reactive statement ensures that the selected component is updated dynamically
  $: CurrentComponent = components[selectedComponent];
</script>

<main>
  <h1>Interview Preparation</h1>
  <select bind:value={selectedComponent}>
    <option value="Chart">Chart</option>
    <option value="AccessibleChart">Accessible Chart</option>
    <option value="ReactiveDataStory">Reactive Data Story</option>
    <option value="ReactiveStores">Reactive Stores</option>
    <option value="Mapping">Mapping</option>
  </select>

  <!-- Dynamic Component Rendering -->
  <svelte:component this={CurrentComponent} />
</main>

<style>
  main {
    min-width: 80%;
    margin: auto;
    text-align: center;
  }
  select {
    margin: 20px;
    padding: 10px;
    font-size: 16px;
  }
</style>

<link
    href="https://api.mapbox.com/mapbox-gl-js/v2.15.0/mapbox-gl.css"
    rel="stylesheet"
/>