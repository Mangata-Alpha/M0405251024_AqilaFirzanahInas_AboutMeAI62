<script lang="ts">
  type Props = {
    id?: string;
    harapan?: string;
    signature?: string;
    role?: string;
  };

  let {
    id = 'kesan',
    harapan = 'Untuk siapa pun yang membaca ini: jangan takut memulai dari yang belum rapi. Garis bantu bisa ditambahkan belakangan — yang penting berani menggambar garis pertama.',
    signature = 'Aqila Firzanah Inas',
    role = 'Mahasiswa Kecerdasan Buatan · IPB University',
  }: Props = $props();
</script>

<section {id} class="relative overflow-hidden border-t border-ink/15 bg-warm-white blueprint-overlay px-6 py-20 md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto max-w-5xl">

    <!-- Section Heading -->
    <header class="mb-12">
      <div class="flex flex-wrap items-center gap-3">
        <span class="inline-flex items-center gap-2 border border-ink/20 bg-warm-white px-3.5 py-1.5 text-kicker text-ink">
          <span class="register-mark" aria-hidden="true"></span>
          <span>03 / HARAPAN</span>
        </span>
        <span class="line-guide max-w-28 flex-1"></span>
      </div>
      <h2 class="mt-4 font-space text-3xl font-bold tracking-tight text-ink sm:text-4xl md:text-5xl">
        Harapan untuk Masa Depan
      </h2>
    </header>

    <!-- Highlighted Quote Card -->
    <div class="corner-brackets relative border border-ink/15 bg-warm-white p-8 shadow-sm md:p-12">
      
      <!-- Big Decorative Quote Mark -->
      <span
        aria-hidden="true"
        class="pointer-events-none absolute -top-8 left-4 z-0 font-space font-bold text-vermilion/15 select-none md:-top-12 md:left-8"
        style="font-size: clamp(6rem, 12dvw, 10rem); line-height: 1;"
      >
        &ldquo;
      </span>

      <div class="relative z-10">

        <blockquote class="font-space text-xl font-medium leading-relaxed text-ink md:text-2xl lg:text-3xl">
          &ldquo;{harapan}&rdquo;
        </blockquote>

        <div class="line-guide my-8"></div>

        <!-- Signature Block -->
        <div class="flex flex-col items-end gap-1 text-right">
          <span class="diagonal-ink mb-1 h-0.5 w-20 -rotate-2 bg-vermilion" aria-hidden="true"></span>
          <cite class="font-space text-xl font-bold not-italic tracking-tight text-ink md:text-2xl">
            {signature}
          </cite>
          <p class="font-outfit text-sm text-ink/65">
            {role}
          </p>
          <span class="tag-constructive mt-2 !text-[0.6rem]">
            Angkatan 62
          </span>
        </div>
      </div>
    </div>
  </div>
</section>