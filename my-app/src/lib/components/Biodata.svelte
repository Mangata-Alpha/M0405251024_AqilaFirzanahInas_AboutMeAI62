<script lang="ts">
  import defaultPhoto from '$lib/assets/profil.png';

  type BioField = { label: string; value: string; icon?: string };
  type Social = { platform: string; label: string; url: string; handle: string };

  type Props = {
    id?: string;
    name?: string;
    tagline?: string;
    fields?: BioField[];
    socials?: Social[];
    photoSrc?: string;
    photoAlt?: string;
  };

  let {
    id = 'biodata',
    name = 'Aqila Firzanah Inas',
    tagline = 'Pada akhirnya, semua yang sulit perlu dijalani untuk bisa terus melangkah ke depan.',
    fields = [
      { label: 'Program Studi', value: 'Kecerdasan Buatan' },
      { label: 'Universitas', value: 'IPB University' },
      { label: 'Angkatan', value: '62' },
      { label: 'NIM', value: 'M0405251024' },
      { label: 'Kelompok', value: 'Amber' },
      { label: 'Tempat, Tanggal Lahir', value: 'Jakarta, 1 Agustus 2007' },
      { label: 'Domisili', value: 'Bogor, Jawa Barat' },
      { label: 'Hobi', value: 'Main game, menggambar' },
    ],
    socials = [
      { platform: 'Instagram', label: 'IG', url: 'https://instagram.com/qilafinas', handle: '@qilafinas' },
      { platform: 'LinkedIn', label: 'in', url: 'https://www.linkedin.com/in/aqila-firzanah-inas-0a37b634a/', handle: 'Aqila Firzanah Inas' },
    ],
    photoSrc = defaultPhoto,
    photoAlt = 'Foto profil Aqila Firzanah',
  }: Props = $props();
</script>

<section {id} class="relative border-t border-ink/15 bg-warm-white blueprint-overlay px-6 py-20 md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto max-w-5xl">

    <!-- Section Heading -->
    <header class="mb-12">
      <div class="flex flex-wrap items-center gap-3">
        <span class="inline-flex items-center gap-2 border border-ink/20 bg-warm-white px-3.5 py-1.5 text-kicker text-ink">
          <span class="register-mark" aria-hidden="true"></span>
          <span>02 / BIODATA DIRI</span>
        </span>
        <span class="line-guide max-w-28 flex-1"></span>
      </div>
      <h2 class="mt-4 font-space text-3xl font-bold tracking-tight text-ink sm:text-4xl md:text-5xl">
        Profil Pribadi
      </h2>
    </header>

    <div class="bio-grid">

      <div class="order-1">
        <div class="border-b border-ink/15 pb-5">
          <span class="text-kicker text-ink/50">Nama Lengkap</span>
          <h3 class="mt-1 font-space text-2xl font-bold tracking-tight text-ink md:text-3xl">{name}</h3>
          <p class="mt-2 max-w-[44ch] font-outfit italic text-ink/75">
            &ldquo;{tagline}&rdquo;
          </p>
        </div>

        <dl class="mt-6 divide-y divide-dashed divide-ink/20 border-t border-b border-ink/15">
          {#each fields as field (field.label)}
            <div class="bio-row transition-colors hover:bg-ink/[0.03] px-1">
              <dt class="text-kicker !tracking-[0.16em] text-ink/65">{field.label}</dt>
              <dd class="font-outfit font-semibold text-ink sm:text-base">{field.value}</dd>
            </div>
          {/each}
        </dl>

        <!-- Kontak medsos -->
        <div class="mt-8 flex flex-wrap items-center gap-4">
          <div class="flex items-center gap-2">
            <span class="register-mark" aria-hidden="true"></span>
            <span class="text-kicker text-ink/70">Terhubung:</span>
          </div>
          <ul class="flex flex-wrap items-center gap-3">
            {#each socials as social (social.platform)}
              <li>
                <a
                  href={social.url}
                  target="_blank"
                  rel="noreferrer noopener"
                  aria-label="{social.platform} ({social.handle})"
                  class="corner-brackets group flex items-center gap-2 border border-ink/30 bg-warm-white px-3 py-1.5 text-xs font-bold tracking-wide text-ink transition-all
                         hover:border-vermilion hover:bg-vermilion hover:text-warm-white
                         focus-visible:border-vermilion focus-visible:bg-vermilion focus-visible:text-warm-white"
                >
                  <span class="font-space uppercase">{social.label}</span>
                  <span class="font-outfit font-normal text-ink/70 group-hover:text-warm-white">{social.platform}</span>
                  <span aria-hidden="true" class="text-[0.65rem] opacity-60 group-hover:opacity-100">↗</span>
                </a>
              </li>
            {/each}
          </ul>
        </div>
      </div>

      <!-- ===== KANAN: foto dengan bingkai clip-art ===== -->
      <div class="relative order-2">
        <div class="photo-frame-backdrop"></div>
        <div class="corner-brackets photo-frame shadow-md">
          <img src={photoSrc} alt={photoAlt} loading="lazy" />
        </div>

        <!-- Label dekoratif -->
        <span
          class="tag-constructive absolute -bottom-3 left-0 -rotate-3 bg-warm-white !text-[0.55rem] sm:!text-[0.625rem] shadow-xs"
        >
          AI Student · {new Date().getFullYear()}
        </span>
      </div>
    </div>
  </div>
</section>