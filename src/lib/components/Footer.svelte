<footer class="footer">
  <div class="footer-content">
    <div class="logos">
      <img src="/icons/nsbe.webp" alt="NSBE logo" class="logo invert" />
      <div class="divider"></div>
      <img src="/icons/utnsbe.png" alt="UT NSBE logo" class="logo invert" />
    </div>

    <nav class="links">
      <a href="/">Home</a>
      <a href="/chapter-info">Chapter Info</a>
      <a href="/officers">Officers</a>
    </nav>

    <p class="copyright">
      © {new Date().getFullYear()} Texas NSBE. All rights reserved.
    </p>
  </div>
</footer>

<style lang="scss">
.footer {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  background-color: #f4eed7; // sand tone
  color: #000;
  padding: 2rem 1rem 1.5rem;
  display: flex;
  justify-content: center;
  border-top: 2px solid rgba(0, 0, 0, 0.1);
}

.footer-content {
  max-width: 1100px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  text-align: center;
}

.logos {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;

  .divider {
    width: 1px;
    height: 30px;
    background: #000;
    opacity: 0.7;
  }

  .logo {
    height: 40px;
    filter: invert(1);
  }
}

.links {
  display: flex;
  gap: 1.5rem;
  margin: 0.75rem 0;

  a {
    text-decoration: none;
    color: #000;
    font-weight: 600;
    transition: color 0.2s ease;

    &:hover {
      color: #b5651d; // orange accent
    }
  }
}

.copyright {
  font-size: 0.9rem;
  opacity: 0.7;
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .links {
    flex-wrap: wrap;
    gap: 1rem;
  }

  .logo {
    height: 30px;
  }

  .divider {
    height: 25px;
  }
}
</style>