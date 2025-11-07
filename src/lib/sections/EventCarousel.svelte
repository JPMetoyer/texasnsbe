<script lang="ts">
  import { onMount, onDestroy } from 'svelte';

  type Slide = { src: string; alt?: string };

  // Photos live here — replace with your own file names
  const slides: Slide[] = [
    { src: '/carousel/1.jpg', alt: 'NSBE GBM group photo' },
    { src: '/carousel/2.jpg', alt: 'NSBE tote bag painting night' },
    { src: '/carousel/3.jpg', alt: 'NSBE members networking' },
    { src: '/carousel/4.jpg', alt: 'NSBE members networking' },
    { src: '/carousel/5.jpg', alt: 'NSBE members networking' },
        { src: '/carousel/6.jpg', alt: 'NSBE members networking' }



  ];

  // Carousel behavior
  let idx = 0;
  let timer: ReturnType<typeof setInterval> | null = null;
  let paused = false;
  const intervalMs = 4000;

  function start() {
    if (timer) clearInterval(timer);
    if (slides.length <= 1) return;
    timer = setInterval(() => {
      if (!paused) idx = (idx + 1) % slides.length;
    }, intervalMs);
  }

  onMount(start);
  onDestroy(() => timer && clearInterval(timer));
</script>

<section class="gallery" aria-label="Texas NSBE event photos">
  <header class="hdr">
    <p class="eyebrow">Capturing Memories!</p>
    <h2>Event Photos</h2>
  </header>

  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div
    class="viewport"
    on:mouseenter={() => (paused = true)}
    on:mouseleave={() => (paused = false)}
  >
    <div class="track" style={`transform: translateX(-${idx * 100}%);`}>
      {#each slides as s (s.src)}
        <figure class="slide">
          <img src={s.src} alt={s.alt ?? ''} loading="lazy" />
        </figure>
      {/each}
    </div>
  </div>

  {#if slides.length > 1}
    <div class="dots">
      {#each slides as _, i}
        <!-- svelte-ignore element_invalid_self_closing_tag -->
        <button
          class="dot"
          class:active={i === idx}
          aria-label={`Go to slide ${i + 1}`}
          on:click={() => (idx = i)}
        />
      {/each}
    </div>
  {/if}
</section>

<style lang="scss">
.gallery {
  padding: 2.5rem 1rem 3rem;
  background:
    radial-gradient(circle at 1px 1px, rgba(0,0,0,0.08) 1px, transparent 1px) repeat;
  background-size: 22px 22px;
}

.hdr {
  text-align: center;
  margin-bottom: 1.25rem;

  .eyebrow {
    text-transform: uppercase;
    letter-spacing: .15em;
    font-weight: 800;
    color: #4b4b4b;
    margin-bottom: .25rem;
  }
  h2 {
    font-size: clamp(1.8rem, 4.5vw, 3.2rem);
    font-weight: 900;
    color: #000;
    margin: 0;
    text-shadow: 0 2px 0 rgba(0,0,0,.06);
  }
}

.viewport {
  max-width: 1200px;
  margin: 0 auto;
  border-radius: 1.2rem;
  overflow: hidden;
  box-shadow: 0 16px 50px rgba(0,0,0,.12);
  background: #fff;
}

.track {
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: 100%;
  transition: transform 550ms cubic-bezier(.22,.85,.25,1);
}

.slide {
  margin: 0;
  padding: clamp(12px, 2vw, 20px);
}
.slide img {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;
  border-radius: 1.1rem;
  display: block;
}

.dots {
  display: flex;
  justify-content: center;
  gap: .5rem;
  margin-top: .9rem;
}
.dot {
  width: 9px; height: 9px; border-radius: 50%;
  background: #c6a45b;
  opacity: .45;
  border: none;
  cursor: pointer;
  transition: opacity .2s ease, transform .2s ease;
}
.dot.active {
  opacity: 1;
  transform: scale(1.1);
}

@media (max-width: 640px) {
  .slide { padding: 12px; }
  .viewport { border-radius: .9rem; }
  .slide img { border-radius: .9rem; }
}

@media (prefers-reduced-motion: reduce) {
  .track { transition: none !important; }
}
</style>