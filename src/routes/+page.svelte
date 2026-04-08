<!-- src/routes/+page.svelte -->
<script lang="ts">
  import Hero from '$lib/sections/Hero.svelte';
    import Mission from '$lib/sections/Mission.svelte';

   import Slides from '$lib/sections/Slides.svelte';
   import Calendar from '$lib/sections/Calendar.svelte';
   import EventCarousel from '$lib/sections/EventCarousel.svelte';
    import MembershipCta from '$lib/sections/MembershipCta.svelte';
    import Leaderboard from '$lib/sections/Leaderboard.svelte';

  import type { Gbm } from '../lib/types/gmb';

  const gbms: Gbm[] = [
    {
      number: 12,
      date: 'APR 7 2026', // fill exact date
      title: 'General Body Meeting #12',
      slidesUrl: 'https://docs.google.com/presentation/d/1c4FsWUX1HOlW_J5hkuLSGC40NfXfXRNFEVO6HeoElhs/edit?usp=sharing',
      coverSrc: '/slides/gm12.png'
    },
    {
      number: 11,
      date: 'MAR 24 2026',
      title: 'General Body Meeting #11',
      slidesUrl: 'https://docs.google.com/presentation/d/1uCVfOi2xZZn2kdjYhGIO74kyoe9xYxow6XIT_qgxCEc/edit',
      coverSrc: '/slides/gm11.png'
    },
    {
      number: 10,
      date: 'MARCH 10 2026',
      title: 'General Body Meeting #10',
      slidesUrl: 'https://docs.google.com/presentation/d/174s5KonpMJciZrQoDjYs7ZEuynBWXosn/edit?usp=sharing&ouid=112665083702612417424&rtpof=true&sd=true',
      coverSrc: '/slides/gm10.png'
    }
  ];
</script>

<Hero title="Welcome to Texas NSBE" videoSrc="/content/nsbevid.mp4" />

<Mission />
<Calendar />
<Leaderboard />


<div id="chapterinfo"></div>
<Slides items={gbms} />



<EventCarousel />

<MembershipCta
  formUrl="https://YOUR_GOOGLE_FORM_LINK"
  duesUrl="https://YOUR_PAY_DUES_LINK"
  shirtSrc="/content/shirts.png"
/>

