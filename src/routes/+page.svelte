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
      number: 8,
      date: 'FEB 10 2026', // fill exact date
      title: 'General Body Meeting #8',
      slidesUrl: 'https://docs.google.com/presentation/d/1cwvFSY2EYTX76qNTryisqyRCw1--28VaZPy5qjthvi0/edit?usp=sharing',
      coverSrc: '/slides/gm8.png'
    },
    {
      number: 7,
      date: 'DEC 2 2025',
      title: 'General Body Meeting #7',
      slidesUrl: 'https://docs.google.com/presentation/d/1KvktUV5iAP34FDrIsn_qTJU0IuO7lvszdXG2ljtqXl0/edit?usp=sharing',
      coverSrc: '/slides/gm7.png'
    },
    {
      number: 6,
      date: 'NOV 18 2025',
      title: 'General Body Meeting #6',
      slidesUrl: 'https://docs.google.com/presentation/d/1EWGdOcBiJ7Nj0QHRpmt71qWv1IxsYrlt1rmyou05HKw/edit?usp=sharing',
      coverSrc: '/slides/gm6.png'
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

