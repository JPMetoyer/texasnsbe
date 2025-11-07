<script lang="ts">
  import type { Gbm } from '../types/gmb';
  export let items: Gbm[] = [];
</script>

<section class="gbms">
  <div class="hdr">
    <p class="eyebrow">MISSED THE MEETING?</p>
    <h2>Recent GBMs</h2>
  </div>

  <div class="grid">
    {#each items as it}
      <a class="card" href={it.slidesUrl} target="_blank" rel="noopener noreferrer"
         aria-label={`Open slides for ${it.title}`}>
        <div class="badge">GBM #{it.number}</div>
        <div class="cover"><img src={it.coverSrc} alt="" /></div>
        <div class="meta">
          <span class="date">{it.date}</span>
          <h3 class="title">{it.title}</h3>
          <span class="cta">View presentation slides</span>
        </div>
      </a>
    {/each}
  </div>
</section>

<style lang="scss">
.gbms {
  padding: 2.5rem 1rem 3rem;
  max-width: 1200px;
  margin: 0 auto;
}

.hdr {
  text-align: center;
  margin-bottom: 1.25rem;

  .eyebrow {
    letter-spacing: .15em;
    text-transform: uppercase;
    font-weight: 700;
    color: #5a5a5a;
    margin: 0 0 .25rem;
  }
  h2 {
    margin: 0;
    font-size: clamp(1.8rem, 4vw, 3rem);
    font-weight: 900;
    color: #000;
    text-shadow: 0 2px 0 rgba(0,0,0,.06);
  }
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.25rem;
}

/* Card as a link */
.card {
  position: relative;
  display: grid;
  grid-template-rows: auto auto;
  background: #fff;
  border: 1px solid #E5D9B8; /* sand border */
  border-radius: 1.25rem;
  overflow: hidden;
  text-decoration: none;
  color: inherit;
  box-shadow: 0 10px 30px rgba(0,0,0,.06);
  transition: transform .18s ease, box-shadow .18s ease;

  &:hover {
    transform: translateY(-4px);
    box-shadow: 0 16px 40px rgba(0,0,0,.12);
  }
}

.badge {
  position: absolute;
  top: .75rem; left: .75rem;
  background: #B5651D;        /* warm brown/orange chip */
  color: #fff;
  font-weight: 800;
  font-size: .9rem;
  padding: .35rem .6rem;
  border-radius: .9rem;
  z-index: 2;
}

.cover {
  aspect-ratio: 16/9;
  background: #f4f4f4;
  overflow: hidden;
}
.cover img {
  width: 100%; height: 100%;
  object-fit: cover;
  display: block;
}

.meta {
  background: #fff;
  padding: 1rem 1.1rem 1.1rem;
  border-top: 1px solid #eee;
  display: grid;
  gap: .35rem;
}

.date {
  font-size: .85rem;
  font-weight: 800;
  letter-spacing: .08em;
  color: #6b6b6b;
}

.title {
  margin: 0;
  font-size: 1.05rem;
  line-height: 1.25;
  font-weight: 800;
  color: #111;
}

.cta {
  font-size: .95rem;
  color: #333;
  opacity: .85;
}
</style>