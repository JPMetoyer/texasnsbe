<script lang="ts">
  import Navbar from '$lib/components/Navbar.svelte';
  import Footer from '$lib/components/Footer.svelte';
  import '$lib/styles/global.scss';

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href="/icons/utnsbe.png" />
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" >
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
</svelte:head>

<Navbar />

<main id="page">
  {@render children()}
</main>

<Footer />