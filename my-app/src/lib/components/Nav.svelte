<script lang="ts">
  type NavLink = { href: string; label: string };

  const links: NavLink[] = [
    { href: '#beranda', label: 'Beranda' },
    { href: '#tentang', label: 'Tentang' },
    { href: '#biodata', label: 'Biodata' },
    { href: '#karya', label: 'Karya' },
    { href: '#kontak', label: 'Kontak' },
  ];

  // -- state (Svelte 5 runes) -------------------------------------
  let open = $state(false);
  let progress = $state(0);
  let activeHref = $state<string>('#beranda');

  function toggleMenu() {
    open = !open;
  }

  function closeMenu() {
    open = false;
  }

  function handleLinkClick(href: string) {
    activeHref = href;
    closeMenu();
  }

  function updateScrollProgress() {
    const doc = document.documentElement;
    const scrollable = doc.scrollHeight - doc.clientHeight;
    progress = scrollable > 0 ? (doc.scrollTop / scrollable) * 100 : 0;
  }

  function handleKeydown(e: KeyboardEvent) {
    if (e.key === 'Escape' && open) closeMenu();
  }

  // Lifecycle: scroll listener + keyboard + body scroll lock,
  // dibungkus $effect supaya otomatis dibersihkan (Svelte 5 runes).
  $effect(() => {
    updateScrollProgress();
    window.addEventListener('scroll', updateScrollProgress, { passive: true });
    window.addEventListener('keydown', handleKeydown);
    return () => {
      window.removeEventListener('scroll', updateScrollProgress);
      window.removeEventListener('keydown', handleKeydown);
    };
  });

  $effect(() => {
    document.body.style.overflow = open ? 'hidden' : '';
  });
</script>

<!-- ============ TOP BAR (desktop + mobile) ============ -->
<header class="nav-shell">
  <div class="mx-auto flex h-full max-w-6xl items-center justify-between px-6 md:px-16 lg:px-32">

    <!-- Monogram / logo mark -->
    <a href="#beranda" class="corner-brackets flex items-center gap-2 p-1" onclick={() => handleLinkClick('#beranda')}>
      <span class="font-bold tracking-tight">AF</span>
      <span class="register-mark" aria-hidden="true"></span>
    </a>

    <!-- Desktop links -->
    <ul class="hidden items-center gap-8 md:flex">
      {#each links as link, i (link.href)}
        <li class="flex items-center gap-8">
          <a
            href={link.href}
            class="underline-sketch text-kicker !tracking-[0.2em]"
            aria-current={activeHref === link.href ? 'true' : undefined}
            onclick={() => handleLinkClick(link.href)}
          >
            {link.label}
          </a>
          {#if i < links.length - 1}
            <span class="h-4 w-px bg-ink/20" aria-hidden="true"></span>
          {/if}
        </li>
      {/each}
    </ul>

    <!-- Mobile hamburger (goresan sketsa 3 garis) -->
    <button
      type="button"
      class="relative z-50 flex h-9 w-9 flex-col items-center justify-center gap-1.5 md:hidden"
      aria-expanded={open}
      aria-controls="mobile-menu"
      aria-label={open ? 'Tutup menu' : 'Buka menu'}
      onclick={toggleMenu}
    >
      <span
        class="h-0.5 w-6 bg-ink transition-transform duration-300 sketch-wobble"
        style="transform: {open ? 'translateY(7px) rotate(45deg)' : 'none'}"
      ></span>
      <span
        class="h-0.5 w-6 bg-ink transition-opacity duration-200 sketch-wobble"
        class:opacity-0={open}
      ></span>
      <span
        class="h-0.5 w-6 bg-ink transition-transform duration-300 sketch-wobble"
        style="transform: {open ? 'translateY(-7px) rotate(-45deg)' : 'none'}"
      ></span>
    </button>
  </div>

  <!-- Garis bantu: progres baca sebagai penunjuk posisi di halaman -->
  <div class="nav-progress" style="transform: scaleX({progress / 100})" aria-hidden="true"></div>
</header>

<!-- ============ MOBILE FULL-SCREEN PANEL ============ -->
<div
  id="mobile-menu"
  class="nav-mobile-panel"
  class:is-open={open}
  inert={!open}
>
  <!-- Aksen diagonal konstruktivis -->
  <span class="pointer-events-none absolute left-0 top-1/3 h-1.5 w-20 -rotate-6 bg-vermilion" aria-hidden="true"></span>
  <span class="pointer-events-none absolute right-6 bottom-24 h-1.5 w-14 bg-constructive" aria-hidden="true"></span>

  <nav aria-label="Navigasi utama">
    <ol class="flex flex-col gap-6">
      {#each links as link, i (link.href)}
        <li class="flex items-center gap-4">
          <span class="text-runner">0{i + 1}</span>
          <span class="line-guide max-w-6 flex-1" aria-hidden="true"></span>
          <a
            href={link.href}
            class="text-4xl font-bold tracking-tight"
            onclick={() => handleLinkClick(link.href)}
          >
            {link.label}
          </a>
        </li>
      {/each}
    </ol>
  </nav>

  <div class="flex items-center justify-between">
    <span class="tag-constructive">AI · Machine Learning</span>
    <span class="text-kicker">Aqila Firzanah</span>
  </div>
</div>