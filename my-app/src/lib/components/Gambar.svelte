<script lang="ts">
  import candle from '$lib/assets/galeri/Little Candle in Penrose.jpg';
  import remembrance from '$lib/assets/galeri/Remembrance.png';
  import returne from '$lib/assets/galeri/Return.png';
  import rukkha from '$lib/assets/galeri/Rukkha redraw.png';
  import wonder from '$lib/assets/galeri/Forest_wonder.jpg';
  import shin from '$lib/assets/galeri/Redraw Shinichi.png';
  import poster from '$lib/assets/galeri/Poster.png';
  import sketch from '$lib/assets/galeri/Moon Silhouette Looking Upon Crow.png';

  type GalleryImage = { src: string; alt: string };

  type Props = {
    id?: string;
    title?: string;
    images?: GalleryImage[];
  };

  let {
    id = 'pojok-gambar',
    title = 'Pojok Gambar',
    images = [
      { src: candle, alt: 'Little Candle in Penrose' },
      { src: remembrance, alt: 'Remembrance' },
      { src: returne, alt: 'Return' },
      { src: rukkha, alt: 'Rukkha Redraw' },
      { src: wonder, alt: 'Forest Wonder' },
      { src: shin, alt: 'Redraw Shinichi' },
      { src: poster, alt: 'Poster Desain' },
      { src: sketch, alt: 'Moon Silhouette Looking Upon Crow' },
    ],
  }: Props = $props();

  function blockContextMenu(e: MouseEvent) {
    e.preventDefault();
  }
</script>

<section
  {id}
  class="relative border-t border-ink/15 bg-vermilion blueprint-overlay px-6 py-20 md:px-16 md:py-28 lg:px-32"
>
  <div class="mx-auto max-w-5xl">

    <!-- Section Heading -->
    <header class="mb-10 flex flex-wrap items-center gap-3 md:mb-14">
      <span class="inline-flex items-center gap-2 bg-warm-white px-3.5 py-1.5 text-kicker text-ink shadow-sm">
        <span class="register-mark" aria-hidden="true"></span>
        <span>04 / {title.toUpperCase()}</span>
      </span>
      <span class="line-guide max-w-28 flex-1 border-warm-white/40"></span>
    </header>

    <!-- Grid masonry: ukuran 5% lebih kecil dengan w-[95%] mx-auto -->
    <div
      class="columns-2 gap-4 sm:columns-3 lg:columns-4"
      oncontextmenu={blockContextMenu}
    >
      {#each images as image (image.src + image.alt)}
        <figure class="group mb-4 w-[95%] mx-auto break-inside-avoid overflow-hidden border border-ink/20 bg-warm-white p-1.5 shadow-md transition-all duration-300 hover:shadow-xl">
          <div class="overflow-hidden bg-ink/5">
            <img
              src={image.src}
              alt={image.alt}
              loading="lazy"
              draggable="false"
              class="block w-full select-none object-cover transition-transform duration-500 group-hover:scale-[1.03]
                     [-webkit-touch-callout:none] [-webkit-user-drag:none]"
            />
          </div>
        </figure>
      {/each}
    </div>

  </div>
</section>