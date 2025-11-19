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
      number: 5,
      date: 'MAR 2025', // fill exact date
      title: 'General Body Meeting #5',
      slidesUrl: 'https://docs.google.com/presentation/d/1HLBdwAjDq6nbf_ntHZN9Pk0TtBBVzbIj-8XWoyUyM4Y/edit?slide=id.g39f108ff632_0_26#slide=id.g39f108ff632_0_26',
      coverSrc: '/slides/gm5.png'
    },
    {
      number: 4,
      date: 'FEB 2025',
      title: 'General Body Meeting #4',
      slidesUrl: 'https://docs.google.com/presentation/d/1ixWWS_FOLT-fcWERIpbIQH4u7cs2GPA1TtDCr8dsTwg/edit?slide=id.g38e13324572_0_141#slide=id.g38e13324572_0_141',
      coverSrc: '/slides/gm4.png'
    },
    {
      number: 3,
      date: 'FEB 2025',
      title: 'General Body Meeting #3',
      slidesUrl: 'https://docs.google.com/presentation/d/15NQ2NVtrIQV6A6hy6im4vQSRaeBQR2AQ3KYDTjv3_h4/edit',
      coverSrc: '/slides/gm3.png'
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

