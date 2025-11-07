<script lang="ts">
  export let title = 'Welcome to Texas NSBE';
  export let videoSrc = '/content/nsbevid.mp4';
</script>

<section class="hero">
  <div class="heading">
    <h1>{title}</h1>
  </div>

  <div class="video-wrap">
    <div class="frame">
      <video
        src={videoSrc}
        autoplay
        loop
        muted
        playsinline
      ></video>
    </div>
  </div>
</section>

<style lang="scss">
.hero {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  padding: 6.5rem 0 2.5rem;
  display: grid;
  gap: 1.25rem;
  place-items: center;
  background: linear-gradient(180deg, #F4EBD0 0%, #fff 100%);
  overflow: hidden;
}

/* Heading */
.heading {
  text-align: center;
}

h1 {
  font-size: clamp(2rem, 6vw, 3.5rem);
  font-weight: 800;
  letter-spacing: 0.02em;
  margin: 0;
  color: #000;
  animation: rise 600ms ease-out 1 both;
}

/* Video container */
.video-wrap {
  width: 100%;
  max-width: 1100px;
  display: flex;
  justify-content: center;
}

.frame {
  position: relative;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 18px 40px rgba(0,0,0,.10);
  background: #000;
  animation: float-in 700ms cubic-bezier(.2,.8,.2,1) 1 120ms both;
  width: 95%; /* adds slight breathing room by default */
}

/* Video styling */
video {
  display: block;
  width: 100%;
  height: auto;
  aspect-ratio: 16 / 9;
  object-fit: cover;
  border-radius: 1rem;
}

/* Motion safety */
@media (prefers-reduced-motion: reduce) {
  h1, .frame { animation: none !important; }
}

/* Keyframes */
@keyframes rise {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes float-in {
  from { opacity: 0; transform: translateY(14px) scale(.98); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}

/* Responsive */
@media (max-width: 900px) {
  .frame {
    width: 92%;
  }
}

@media (max-width: 640px) {
  .hero {
    padding: 6rem 0 2rem;
  }
  .frame {
    width: 88%;
    border-radius: 0.9rem;
  }
}
</style>