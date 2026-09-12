<script lang="ts">
  import defaultPhoto from '$lib/assets/profil.png';

  type BioField = { label: string; value: string };

  type Props = {
    id?: string;
    name?: string;
    tagline?: string;
    fields?: BioField[];
    photoSrc?: string;
    photoAlt?: string;
  };

  let {
    id = 'biodata',
    name = 'Aqila Firzanah',
    tagline = 'Menyusun data jadi rapi, satu garis bantu pada satu waktu.',
    fields = [
      { label: 'Program Studi', value: 'Kecerdasan Artifisial' },
      { label: 'Universitas', value: 'IPB University' },
      { label: 'Angkatan', value: '62' },
      { label: 'NIM', value: 'M0405251024' },
      { label: 'Lokasi', value: 'Indonesia' },
    ],
    photoSrc = defaultPhoto,
    photoAlt = 'Foto profil',
  }: Props = $props();
</script>

<section {id} class="relative border-t border-ink/15 px-6 py-20 md:px-16 md:py-28 lg:px-32">
  <div class="mx-auto max-w-5xl">

    <!-- Kicker -->
    <div class="mb-10 flex items-center gap-3 md:mb-14">
      <span class="register-mark" aria-hidden="true"></span>
      <span class="text-kicker">Biodata</span>
      <span class="line-guide max-w-24 flex-1"></span>
    </div>

    <!-- Grid asimetris: biodata (kiri) + foto ala kartu ID (kanan) —
         rasio ini dipertahankan sejak mobile, tidak pernah jadi 1 kolom -->
    <div class="bio-grid">

      <!-- ===== KIRI: biodata ===== -->
      <div class="order-1">
        <h3 class="text-2xl font-bold tracking-tight md:text-3xl">{name}</h3>
        <p class="mt-2 max-w-[42ch] text-ink/70">{tagline}</p>

        <dl class="mt-6 border-t border-ink/15 md:mt-8">
          {#each fields as field, i (field.label)}
            <div class="bio-row">
              <dt class="text-kicker !tracking-[0.18em] text-ink/60">{field.label}</dt>
              <dd class="font-bold">{field.value}</dd>
            </div>
            {#if i < fields.length - 1}
              <div class="line-guide"></div>
            {/if}
          {/each}
        </dl>
      </div>

      <!-- ===== KANAN: foto dengan bingkai clip-art ===== -->
      <div class="relative order-2">
        <div class="corner-brackets photo-frame">
          <img src={photoSrc} alt={photoAlt} loading="lazy" />
        </div>

        <!-- Label kecil "menempel" di bingkai, sedikit miring — aksen konstruktivis -->
        <span
          class="tag-constructive absolute -bottom-3 left-0 -rotate-3 bg-warm-white !text-[0.55rem] sm:!text-[0.625rem]"
        >
          AI · {new Date().getFullYear()}
        </span>
      </div>
    </div>
  </div>
</section>