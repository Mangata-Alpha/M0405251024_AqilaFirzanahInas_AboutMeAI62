<script lang="ts">
  type NavLink = { href: string; label: string };

  const links: NavLink[] = [
    { href: '#beranda', label: 'Beranda' },
    { href: '#tentang', label: 'Tentang' },
    { href: '#biodata', label: 'Biodata' },
    { href: '#kesan', label: 'Harapan' },
    { href: '#pojok-gambar', label: 'Pojok Gambar' },
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

  // Lifecycle: scroll listener + keyboard + body scroll lock + intersection observer
  $effect(() => {
    updateScrollProgress();
    window.addEventListener('scroll', updateScrollProgress, { passive: true });
    window.addEventListener('keydown', handleKeydown);

    // IntersectionObserver to auto-update active nav link based on scroll position
    const observer = new IntersectionObserver(
      (entries) => {
        for (const entry of entries) {
          if (entry.isIntersecting) {
            activeHref = `#${entry.target.id}`;
          }
        }
      },
      {
        rootMargin: '-30% 0px -60% 0px',
        threshold: 0,
      }
    );

    const sections = document.querySelectorAll('section[id]');
    sections.forEach((section) => observer.observe(section));

    return () => {
      window.removeEventListener('scroll', updateScrollProgress);
      window.removeEventListener('keydown', handleKeydown);
      observer.disconnect();
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
    <a href="#beranda" class="corner-brackets flex items-center gap-2 p-1.5 transition-transform hover:scale-105" onclick={() => handleLinkClick('#beranda')}>
      <span class="font-space font-bold tracking-tight text-ink">AF</span>
      <span class="register-mark" aria-hidden="true"></span>
    </a>

    <!-- Desktop links -->
    <nav aria-label="Navigasi Desktop" class="hidden md:block">
      <ul class="flex items-center gap-6 lg:gap-8">
        {#each links as link, i (link.href)}
          <li class="flex items-center gap-6 lg:gap-8">
            <a
              href={link.href}
              class="underline-sketch text-kicker !tracking-[0.2em] transition-colors hover:text-vermilion"
              class:!text-vermilion={activeHref === link.href}
              aria-current={activeHref === link.href ? 'true' : undefined}
              onclick={() => handleLinkClick(link.href)}
            >
              {link.label}
            </a>
            {#if i < links.length - 1}
              <span class="h-3.5 w-px bg-ink/20" aria-hidden="true"></span>
            {/if}
          </li>
        {/each}
      </ul>
    </nav>

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

  <nav aria-label="Navigasi mobile" class="pt-8">
    <ol class="flex flex-col gap-5">
      {#each links as link, i (link.href)}
        <li class="flex items-center gap-4">
          <span class="text-runner">0{i + 1}</span>
          <span class="line-guide max-w-6 flex-1" aria-hidden="true"></span>
          <a
            href={link.href}
            class="font-space text-3xl font-bold tracking-tight transition-colors hover:text-vermilion"
            class:text-vermilion={activeHref === link.href}
            onclick={() => handleLinkClick(link.href)}
          >
            {link.label}
          </a>
        </li>
      {/each}
    </ol>
  </nav>

  <div class="flex items-center justify-between border-t border-ink/15 pt-6">
    <span class="tag-constructive">AI · Machine Learning</span>
    <span class="text-kicker">Aqila Firzanah</span>
  </div>
</div>