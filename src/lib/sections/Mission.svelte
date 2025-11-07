<section class="mission">
  <div class="content">
    <p class="intro">
      The mission of the National Society of Black Engineers is:
    </p>

    <blockquote class="quote">
      <span class="quote-mark left">“</span>
      <p>
        To increase the number of culturally responsible Black engineers who
        excel academically, succeed professionally, and positively impact the
        community.
      </p>
      <span class="quote-mark right">”</span>
    </blockquote>
  </div>
</section>

<style lang="scss">
.mission {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  background-color: #f4eed7; // your site’s sand tone
  color: #111;
  padding: 5rem 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  position: relative;
}

.content {
  max-width: 900px;
  padding: 0 1rem;
}

.intro {
  font-weight: 700;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: #b5651d;
  margin-bottom: 1.5rem;
  font-size: 1.05rem;
}

.quote {
  position: relative;
  font-size: clamp(1.4rem, 3vw, 2rem);
  font-weight: 600;
  line-height: 1.4;
  color: #000;
  font-family: "Inter", sans-serif;
  margin: 0 auto;
  padding: 0 1rem;

  p {
    margin: 0;
  }

  .quote-mark {
    position: absolute;
    font-size: 3rem;
    color: #b5651d;
    font-weight: bold;
    opacity: 0.9;
  }

  .left {
    top: -30px;
    left: -20px;
  }

  .right {
    bottom: -30px;
    right: -20px;
  }
}

/* Responsive tweaks */
@media (max-width: 768px) {
  .mission {
    padding: 3.5rem 1.5rem;
  }

  .quote {
    font-size: 1.25rem;

    .quote-mark {
      font-size: 2rem;
    }
  }
}
</style>