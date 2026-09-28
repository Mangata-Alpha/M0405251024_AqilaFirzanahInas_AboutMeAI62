<script lang="ts">
  import './layout.css';
  import favicon from '$lib/assets/Bebek_sprite.png';
  import Nav from '$lib/components/Nav.svelte';

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
  <title>Aqila Firzanah — Portfolio</title>
  <meta
    name="description"
    content="Portofolio perkenalan Aqila Firzanah, mahasiswa Kecerdasan Artifisial."
  />
</svelte:head>

<a
  href="#konten"
  class="fixed left-4 top-4 z-[60] -translate-y-20 bg-ink px-4 py-2 text-warm-white
         transition-transform focus-visible:translate-y-0"
>
  Lompat ke konten
</a>

<Nav />

<main id="konten" class="relative z-10 min-h-dvh bg-transparent text-ink font-space">
  {@render children()}
</main>