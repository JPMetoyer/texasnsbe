<script lang="ts">
  export let title = 'Join Texas NSBE';
  export let blurb =
    '$25 membership dues unlock your shirt, test bank, conference discounts, voting rights, and invites to socials & more.';
  export let formUrl = 'docs.google.com/forms/d/e/1FAIpQLSdx_JyLmclXt9NF_MTv3pXs1HwDXGqES1LxGhWbspjObOtNPg/viewform?fbclid=PAZXh0bgNhZW0CMTEAAaesC8265qf_IcsLYFqHfBIWEG3ZtdNhN5ZPg5zfOPq6Bo79w1HTioWBFNUhZg_aem_nE8qL5cSrtniQA2SwRvdDA'; // TODO: replace
  export let duesUrl = 'https://utdirect.utexas.edu/nlogon/txshop/item_details.WBX?application_name=ENENGALU&component=0&dept_prefix=E4&item_id=125&cat_seq_chosen=02&subcategory_seq_chosen=000';        // TODO: replace
  export let shirtSrc = '/content/shirts.png';   // TODO: point to your landscape image
</script>

<section class="join">
  <header class="hdr">
    <p class="eyebrow">Become a member</p>
    <h2>{title}</h2>
    <p class="sub">{blurb}</p>
  </header>

  <div class="content">
    <ul class="benefits">
      <li>Free membership shirt</li>
      <li>Access to our online test bank</li>
      <li>NSBE conference discounts</li>
      <li>Voting rights in spring Top-5 elections</li>
      <li>Invites to socials, boat party & more</li>
    </ul>

    <div class="actions">
      <a class="btn outline" href={formUrl} target="_blank" rel="noopener noreferrer" aria-label="Open membership form">
        <span>Membership Form</span>
      </a>
      <a class="btn filled" href={duesUrl} target="_blank" rel="noopener noreferrer" aria-label="Pay membership dues">
        <span>Pay Dues ($25)</span>
      </a>
    </div>
  </div>

  <figure class="shirt">
    <img src={shirtSrc} alt="Texas NSBE 2025–2026 shirt design" loading="lazy" />
  </figure>
</section>

<style lang="scss">

    :global(body) {
  margin: 0;
  padding: 0;
  overflow-x: hidden; // prevents scrollbars caused by gradients or transforms
  background-color: #f4ebd0; // match the sand background
}

.join {
  width: 100%;
  margin: 0 auto;
  text-align: center;
  padding: 2.75rem 1rem 3.25rem;
  background:
    radial-gradient(circle at 1px 1px, rgba(0,0,0,0.08) 1px, transparent 1px) repeat,
    linear-gradient(180deg, #F4EBD0 0%, #fff 100%);
  background-size: 22px 22px, auto;


  @media screen and (max-width: 768px) {
   margin-right: 10rem  !important;
   padding: 0 0 3rem 0;
  }
  
}


.hdr {
  text-align: center;
  margin: 0 auto 1.5rem;
  max-width: 900px;

  .eyebrow {
    margin: 0 0 .35rem;
    text-transform: uppercase;
    letter-spacing: .14em;
    font-weight: 800;
    color: #4b4b4b;
  }
  h2 {
    margin: 0;
    font-size: clamp(1.8rem, 4vw, 2.6rem);
    font-weight: 900;
    color: #000;
    text-shadow: 0 2px 0 rgba(0,0,0,.06);
  }
  .sub {
    margin: .6rem auto 0;
    color: #333;
    max-width: 52ch;
  }
}

.content {
  max-width: 900px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  text-align: center;
}

/* Benefits list */
.benefits {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  grid-template-columns: repeat(2, minmax(220px, 1fr));
  gap: .55rem 1rem;

  @media (max-width: 640px) { grid-template-columns: 1fr; }

  li {
    position: relative;
    padding-left: 1.25rem;
    line-height: 1.45;
    color: #222;

    &::before {
      content: '';
      position: absolute;
      left: 0; top: .45rem;
      width: 8px; height: 8px; border-radius: 50%;
      background: #FFB400; /* gold dot */
    }
  }
}

/* CTA buttons */
.actions {
  display: flex;
  align-items: center;
  gap: .8rem;
  justify-content: flex-start;

  @media (max-width: 860px) { justify-content: center; flex-wrap: wrap; }
}

.btn {
  --radius: 999px;
  --padY: 0.7rem;
  --padX: 1.1rem;

  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: .45rem;
  padding: var(--padY) var(--padX);
  border-radius: var(--radius);
  font-weight: 700;
  text-decoration: none;
  cursor: pointer;
  transition: transform .12s ease, box-shadow .12s ease, background-color .12s ease, color .12s ease;
  border: 1px solid #000;
  font-size: 0.98rem;

  &:active { transform: translateY(1px); }
}

.btn.filled {
  background: #000;
  color: #F4EBD0;

  &:hover { color: #FFB400; }
}

.btn.outline {
  background: transparent;
  color: #000;

  &:hover {
    background: #000;
    color: #F4EBD0;
  }
}

/* Shirt banner */
.shirt {
  max-width: 1200px;
  margin: 1.25rem auto 0;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 16px 40px rgba(0,0,0,.12);
  background: #111;

  @media screen and (max-width:768px) {
    width: 90vw;
  }


  img {
    width: 100%;
    height: auto;
    display: block;
    object-fit: cover;

      @media screen and (max-width:768px) {
    width: 90vw;
  }


  }
}
</style>