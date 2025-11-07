<script lang="ts">
  // Props if you ever want to reuse with different calendars
  export let title = 'Upcoming Events';
  export let src =
    'https://calendar.google.com/calendar/embed?height=400&wkst=1&ctz=America%2FChicago&showTitle=0&showNav=0&showTz=0&showTabs=0&showPrint=0&src=bG9vNG1ldW1mYmg0OTlpcDdyN29mbmV0b2tAZ3JvdXAuY2FsZW5kYXIuZ29vZ2xlLmNvbQ&color=%23F6BF26';
</script>

<section class="calendar-section">
  <div class="hdr">
    <h2>{title}</h2>
    <p class="sub">See what’s coming up for the Texas NSBE chapter.</p>
  </div>

  <div class="frame">
    <!-- eslint-disable-next-line svelte/valid-iframe-title -->
    <!-- svelte-ignore element_invalid_self_closing_tag -->
    <iframe
      class="calendar"
      src={src}
      title="Texas NSBE Google Calendar"
      loading="lazy"
      referrerpolicy="no-referrer-when-downgrade"
    />
  </div>

  <!-- Fallback link if iframes are blocked -->

</section>

<style lang="scss">
.calendar-section {
  padding: 2.5rem 1rem 3rem;
  max-width: 1100px;
  margin: 0 auto;
}

.hdr {
  text-align: center;
  margin-bottom: 1rem;

  h2 {
    margin: 0 0 .35rem;
    font-size: clamp(1.6rem, 3.5vw, 2.2rem);
    font-weight: 800;
    color: #000;
  }
  .sub {
    margin: 0;
    color: #444;
  }
}

/* Responsive iframe wrapper */
.frame {
  border: 1px solid #E5D9B8; /* sand border to match the site */
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0,0,0,.06);
  background: #fff;
}

/* Make the iframe fluid and tall enough without stretching weirdly */
.calendar {
  display: block;
  width: 100%;
  height: clamp(460px, 62vh, 780px);
  border: 0;
}

/* Tighten on very small screens so it doesn’t touch edges visually */
@media (max-width: 640px) {
  .calendar-section { padding-left: .75rem; padding-right: .75rem; }
  .calendar { height: clamp(440px, 65vh, 680px); }
}

/* Roomier on large screens */
@media (min-width: 1024px) {
  .calendar { height: clamp(560px, 60vh, 820px); }
}



</style>