<script lang="ts">
  import myImage from '$lib/assets/Guides.png';
  import Biodata from '$lib/components/Biodata.svelte';

  const meta = {
    year: new Date().getFullYear(),
    role: 'AI Student',
  } as const;

  type Project = {
    index: string;
    title: string;
    stack: string;
    note: string;
  };

  const projects: Project[] = [
    {
      index: '01',
      title: 'Klasifikasi Citra dengan CNN',
      stack: 'Python · TensorFlow',
      note: 'Model pengenal objek sederhana untuk latihan arsitektur convolutional.',
    },
    {
      index: '02',
      title: 'Analisis Sentimen Teks Berbahasa Indonesia',
      stack: 'Python · scikit-learn',
      note: 'Eksperimen pemrosesan bahasa alami pada data ulasan publik.',
    },
    {
      index: '03',
      title: 'Sistem Rekomendasi Sederhana',
      stack: 'Python · Pandas',
      note: 'Pendekatan collaborative filtering untuk studi kasus kelas.',
    },
  ];
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
    <span>Portofolio · {meta.year}</span>
    <span class="hidden sm:inline">{meta.role}</span>
  </div>

  <!-- Portrait -->
  <img
    src={myImage}
    alt="Ilustrasi Aqila Firzanah"
    class="pointer-events-none absolute bottom-0 right-0 z-0
           w-[55%] select-none object-contain opacity-90
           md:w-[38%] lg:w-[28%]"
  />

  <!-- Nama -->
  <div class="relative z-10 flex flex-1 flex-col justify-center">
    <div class="mb-6 flex items-center gap-4 md:mb-10">
      <span class="block-vermilion">Hello</span>
      <span class="rule-ink max-w-32 flex-1"></span>
    </div>

    <h2 class="Introduce">Halo! Namaku...</h2>
    <h1 class="name-introduce">Aqila Firzanah</h1>
  </div>

  <!-- Footer strip -->
  <div class="relative z-10 flex items-end justify-between">
    <span class="tag-constructive">AI · Machine Learning</span>
    <a href="#tentang" class="hidden text-kicker underline-sketch md:inline">Gulir ↓</a>
  </div>
</section>

<!-- ================= TENTANG ================= -->
<section id="tentang" class="relative px-6 py-20 md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto grid max-w-5xl gap-10 md:grid-cols-[minmax(0,7rem)_1fr]">
    <div class="flex items-start gap-4 md:flex-col md:items-start md:gap-2">
      <span class="register-mark" aria-hidden="true"></span>
      <span class="text-kicker">Tentang</span>
    </div>

    <div class="max-w-[62ch]">
      <p class="text-2xl font-bold leading-snug md:text-3xl">
        Mahasiswa Kecerdasan Artifisial yang senang menyusun hal-hal
        rumit jadi rapi, tanpa membuatnya kaku.
      </p>

      <div class="line-guide my-8"></div>

      <p class="text-base leading-relaxed text-ink/80 md:text-lg">
        Aku suka ruang kosong secukupnya dan garis bantu—setipis apa pun—
        karena keduanya membantu tetap tahu arah, baik saat merancang
        model maupun merancang halaman ini sendiri.
      </p>

      <div class="mt-8 flex flex-wrap gap-3">
        <span class="tag-constructive">Machine Learning</span>
        <span class="tag-constructive">Data</span>
        <span class="tag-constructive">Desain Terstruktur</span>
      </div>
    </div>
  </div>
</section>

<Biodata />

<!-- ================= KARYA ================= -->
<section id="karya" class="relative border-t border-ink/15 px-6 py-20 md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto max-w-5xl">
    <div class="mb-12 flex items-end justify-between">
      <h2 class="text-kicker">Karya Terpilih</h2>
      <span class="text-runner hidden sm:inline">{projects.length} proyek</span>
    </div>

    <ol class="flex flex-col">
      {#each projects as project, i (project.index)}
        <li>
          <div class="grid grid-cols-[3rem_1fr] items-baseline gap-4 py-6 md:grid-cols-[4rem_1fr_auto] md:gap-8">
            <span class="text-runner">{project.index}</span>
            <div class="corner-brackets p-3">
              <h3 class="text-lg font-bold md:text-xl">{project.title}</h3>
              <p class="mt-1 text-sm text-ink/70">{project.note}</p>
            </div>
            <span class="text-runner hidden md:inline">{project.stack}</span>
          </div>
          {#if i < projects.length - 1}
            <div class="line-guide"></div>
          {/if}
        </li>
      {/each}
    </ol>
  </div>
</section>

<!-- ================= KONTAK ================= -->
<section id="kontak" class="relative border-t border-ink/15 bg-ink px-6 py-20 text-warm-white md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto flex max-w-5xl flex-col gap-8 md:flex-row md:items-end md:justify-between">
    <div>
      <span class="text-kicker text-warm-white/70">Kontak</span>
      <p class="mt-4 max-w-[38ch] text-3xl font-bold leading-tight md:text-4xl">
        Terbuka untuk kolaborasi dan diskusi seputar AI.
      </p>
    </div>

    <a
      href="mailto:aqila.firzanah@example.com"
      class="block-vermilion w-fit text-sm md:text-base"
    >
      Kirim Email
    </a>
  </div>
</section>