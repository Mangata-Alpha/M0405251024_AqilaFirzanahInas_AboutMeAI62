<script lang="ts">
  import myImage from '$lib/assets/Guides.png';
  import Biodata from '$lib/components/Biodata.svelte';
  import PojokGambar from '$lib/components/Gambar.svelte';
  import Kesan from '$lib/components/Kesan.svelte';

  const meta = {
    year: new Date().getFullYear(),
    role: 'AI Student',
    email: 'zirc87aainas@apps.ipb.ac.id',
  } as const;

  let copied = $state(false);

  async function copyEmail() {
    try {
      await navigator.clipboard.writeText(meta.email);
      copied = true;
      setTimeout(() => {
        copied = false;
      }, 2500);
    } catch {
      // Fallback if clipboard API is restricted
      window.location.href = `mailto:${meta.email}`;
    }
  }
</script>

<!-- ================= HERO ================= -->
<section id="beranda" class="hero">
  <!-- Aksen konstruktivis -->
  <span aria-hidden="true" class="absolute left-0 top-[30%] h-28 w-1.5 bg-vermilion"></span>
  <span aria-hidden="true" class="absolute left-0 top-[44%] h-1.5 w-24 bg-vermilion"></span>
  <span aria-hidden="true" class="absolute right-[44%] top-[22%] h-3 w-3 bg-constructive"></span>
  <span aria-hidden="true" class="absolute bottom-8 right-6 h-1.5 w-16 bg-constructive md:right-16 lg:right-32"></span>

  <!-- Kicker -->
  <div class="relative z-10 flex items-center justify-between text-kicker">
    <span class="hidden items-center gap-2 sm:inline-flex">
      <span class="h-1.5 w-1.5 rounded-full bg-constructive"></span>
      {meta.role} · IPB University · {meta.year}
    </span>
  </div>

  <!-- Portrait -->
  <img
    src={myImage}
    alt="Ilustrasi Aqila Firzanah"
    class="pointer-events-none absolute bottom-0 right-0 z-0
           w-[55%] select-none object-contain opacity-90 transition-transform duration-500 hover:scale-[1.02]
           md:w-[38%] lg:w-[28%]"
  />

  <!-- Nama -->
  <div class="relative z-10 flex flex-1 flex-col justify-center">
    <div class="mb-2 flex items-center gap-3">
      <span class="register-mark" aria-hidden="true"></span>
      <span class="text-kicker !text-ink/60">Pengenalan</span>
    </div>
    <h2 class="Introduce">Halo! Namaku...</h2>
    <h1 class="name-introduce">Aqila Firzanah</h1>
  </div>

  <!-- Footer strip -->
  <div class="relative z-10 flex items-end justify-between border-t border-ink/10 pt-4">
    <div class="flex flex-wrap items-center gap-2">
      <span class="tag-constructive">AI · Machine Learning</span>
      <span class="hidden border border-ink/20 px-3 py-1 text-kicker text-ink/70 sm:inline-block">Creative Explorer</span>
    </div>
    <a href="#tentang" class="text-kicker underline-sketch flex items-center gap-1.5">
      <span>Jelajahi Profil</span>
      <span aria-hidden="true">↓</span>
    </a>
  </div>
</section>

<!-- ================= TENTANG ================= -->
<section id="tentang" class="relative border-t border-ink/15 bg-vermilion blueprint-overlay px-6 py-20 md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto max-w-5xl">
    
    <!-- Section Heading -->
    <header class="mb-12">
      <div class="flex flex-wrap items-center gap-3">
        <span class="inline-flex items-center gap-2 bg-warm-white px-3.5 py-1.5 text-kicker text-ink shadow-sm">
          <span class="register-mark" aria-hidden="true"></span>
          <span>01 / TENTANG SAYA</span>
        </span>
        <span class="line-guide max-w-28 flex-1 border-warm-white/40"></span>
      </div>
      <h2 class="mt-4 font-space text-3xl font-bold tracking-tight text-warm-white sm:text-4xl md:text-5xl">
        Mengenal Lebih Dekat
      </h2>
    </header>

    <!-- Content Card -->
    <div class="grid gap-10 md:grid-cols-[minmax(0,6rem)_1fr]">
      <div class="hidden flex-col items-start gap-3 md:flex">
        <span class="block-vermilion border border-warm-white/30 !bg-warm-white !text-ink">01</span>
        <span class="h-16 w-px bg-warm-white/30"></span>
      </div>

      <div class="corner-brackets max-w-[65ch] bg-warm-white p-6 shadow-md md:p-10">
        <div class="mb-4 inline-flex items-center gap-2 text-kicker text-vermilion">
          <span class="h-2 w-2 bg-vermilion"></span>
          <span>Prinsip & Visi</span>
        </div>

        <p class="font-space text-2xl font-bold leading-snug text-ink md:text-3xl">
          Mahasiswa Kecerdasan Artifisial yang senang membuat hal rumit menjadi sesuatu yang lebih mudah dipahami
        </p>

        <div class="line-guide my-8"></div>

        <div class="space-y-4 font-outfit text-base leading-relaxed text-ink/80 md:text-lg">
          <p>
            Hadapilah semuanya baik susah maupun senang. Karena masalah yang sulit akan memiliki jawaban. Hanya waktu yang membedakannya dengan masalah yang mudah.
          </p>
        </div>

        <!-- Highlighted Topics / Tags -->
        <div class="mt-8 border-t border-ink/10 pt-6">
          <span class="text-kicker mb-3 block text-ink/60">Fokus Pembelajaran:</span>
          <div class="flex flex-wrap gap-2.5">
            <span class="tag-constructive bg-warm-white shadow-xs">Machine Learning</span>
            <span class="tag-constructive bg-warm-white shadow-xs">Data Science</span>
            <span class="tag-constructive bg-warm-white shadow-xs">Problem Solving</span>
            <span class="tag-constructive bg-warm-white shadow-xs">Visual Arts</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ================= BIODATA COMPONENT ================= -->
<Biodata />

<!-- ================= KESAN & HARAPAN COMPONENT ================= -->
<Kesan
  harapan="Terus belajar, berkembang, dan berevolusi seperti AI yang terus berevolusi seiring dengan waktu."
  signature="Aqila Firzanah Inas"
  role="Mahasiswa Kecerdasan Buatan · IPB University"
/>

<!-- ================= POJOK GAMBAR COMPONENT ================= -->
<PojokGambar />


<!-- ================= KONTAK ================= -->
<section id="kontak" class="relative border-t border-ink/15 bg-ink px-6 py-20 text-warm-white md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto max-w-5xl">
    
    <!-- Section Heading -->
    <header class="mb-12">
      <div class="flex flex-wrap items-center gap-3">
        <span class="inline-flex items-center gap-2 border border-warm-white/20 bg-ink px-3.5 py-1.5 text-kicker text-warm-white">
          <span class="register-mark" aria-hidden="true"></span>
          <span>05 / KONTAK</span>
        </span>
        <span class="line-guide max-w-28 flex-1 border-warm-white/20"></span>
      </div>
      <h2 class="mt-4 font-space text-3xl font-bold tracking-tight text-warm-white sm:text-4xl md:text-5xl">
        Kontak melalui
      </h2>
    </header>

    <div class="corner-brackets grid gap-8 border border-warm-white/15 bg-ink/70 p-6 md:grid-cols-[1fr_auto] md:items-center md:p-10">
      <div>
        <span class="text-kicker text-warm-white/60">Email</span>
        <p class="mt-2 font-space text-xl font-bold break-all text-warm-white sm:text-2xl md:text-3xl">
          {meta.email}
        </p>
      </div>

      <div class="flex flex-wrap items-center gap-3">
        <a
          href="mailto:{meta.email}"
          class="block-vermilion flex items-center gap-2 px-5 py-3 text-sm font-bold tracking-wider transition-transform hover:-translate-y-0.5 hover:brightness-110 active:translate-y-0 md:text-base"
        >
          <span>Kirim Email</span>
          <span aria-hidden="true">↗</span>
        </a>

        <button
          type="button"
          onclick={copyEmail}
          class="inline-flex items-center gap-2 border border-warm-white/30 px-4 py-3 text-kicker text-warm-white transition-colors hover:border-warm-white hover:bg-warm-white/10"
        >
          {#if copied}
            <span>✓ Tersalin!</span>
          {:else}
            <span>Salin Email</span>
          {/if}
        </button>
      </div>
    </div>

    <!-- Footer Copyright Note -->
    <div class="mt-14 flex flex-col items-center justify-between gap-4 border-t border-warm-white/10 pt-8 text-center sm:flex-row sm:text-left">
      <span class="text-runner text-warm-white/50">
        © {meta.year} Aqila Firzanah Inas
      </span>
    </div>
  </div>
</section>