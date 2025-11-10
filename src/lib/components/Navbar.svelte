<script lang="ts">
  import { getStores } from '$app/stores';
  const { page } = getStores();

  let toggleMenu = false;
  function handleMenuToggle() {
    toggleMenu = !toggleMenu;
  }

  $: currentPath = $page.url.pathname;
</script>

<!-- svelte-ignore a11y_click_events_have_key_events -->
<nav>
  <a href="/" id="logo">
    <img src="/icons/nsbe.webp" alt="NSBE Logo" class="logo-main" />
    <div class="divider"></div>
    <img src="/icons/utnsbe.png" alt="Texas NSBE Logo" class="logo-ut" />
  </a>

  <!-- Hamburger -->
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div id="menu-toggle" class:active={toggleMenu} on:click={handleMenuToggle}>
    <span></span>
    <span></span>
    <span></span>
  </div>

  <!-- Desktop Nav Links -->
  <div id="links">
    <a href="/" class={currentPath === '/' ? 'selected' : ''}>Home</a>
    <a href="/#chapterinfo" >Chapter Info</a>
    <a href="/officers" class={$page.url.pathname === '/officers' ? 'selected' : ''}>Officers</a>
  </div>

  <!-- Desktop Socials + CTA -->
  <div id="additional">
    <a href="https://www.instagram.com/texasnsbe/" class="social" target="_blank">
      <img src="/icons/insta.png" alt="Instagram" />
    </a>
    <a href="https://www.linkedin.com/company/utnsbe/posts/?feedView=all" class="social" target="_blank">
      <img src="/icons/linkedin.png" alt="LinkedIn" />
    </a>

    <div id="socials" style="margin-right: 0.6rem;">
      <a href="https://nsbemembers.slack.com/signup#/domain-signup" target="_blank">Join our Slack</a>
      <img src="/icons/arrow.png" alt="Arrow" />
    </div>
  </div>

  <!-- Slide-Over Mobile Menu -->
  <div id="menu-links" class:active={toggleMenu}>
    <a href="/" class={currentPath === '/' ? 'selected' : ''} on:click={handleMenuToggle}>Home</a>
    <a href="/#chapterinfo" on:click={handleMenuToggle}>Chapter Info</a>
    <a href="/officers" class={$page.url.pathname === '/officers' ? 'selected' : ''} on:click={handleMenuToggle}>Officers</a>

    <div id="scmedia">
      <a href="https://www.instagram.com/texasnsbe/" class="social" on:click={handleMenuToggle} target="_blank">
        <img src="/icons/insta.png" alt="Instagram" />
      </a>
      <a href="https://www.linkedin.com/company/utnsbe/posts/?feedView=all" class="social" on:click={handleMenuToggle} target="_blank">
        <img src="/icons/linkedin.png" alt="LinkedIn" />
      </a>
    </div>

    <div id="join">
      <a href="https://nsbemembers.slack.com/signup#/domain-signup" on:click={handleMenuToggle} target="_blank">Join our Slack</a>
      <img src="/icons/arrow.png" alt="Arrow" />
    </div>
  </div>
</nav>

<style lang="scss">
@import url('https://api.fontshare.com/v2/css?f[]=satoshi@1&display=swap');
@import url('https://api.fontshare.com/v2/css?f[]=open-sauce-one@400,500,600,700&display=swap');

:global(html),
:global(body) {
  overflow-x: hidden;
}

nav {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  background-color: #F4EBD0;
  padding: 0.3rem 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  height: 5rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  box-sizing: border-box;

  #logo {
    display: flex;
    align-items: center;
    gap: 1rem;

    img.logo-main,
    img.logo-ut {
      height: 4rem;
      width: auto;
      object-fit: contain;
      filter: invert(1);
    }

    .divider {
      width: 2px;
      height: 4rem;
      background-color: #000000;
    }

    img:hover {
      transform: rotate(360deg);
      transition: all 0.8s ease-in-out;
    }
  }

  /* Desktop nav links */
  #links {
    display: flex;
    align-items: center;
    gap: 1.2rem;
    margin-right: 3rem;

    a {
      color: #000;
      font-family: 'satoshi', sans-serif;
      font-weight: 500;
      font-size: 18px;
      text-decoration: none;
      transition: all 200ms ease-in-out;

      &:hover {
        color: #8A5900;
        border-bottom: 1px solid #FFB400;
        transform: translateY(-3px);
      }
    }

    @media screen and (max-width: 1024px) {
      display: none;
    }
  }

  /* Desktop social icons + CTA */
  #additional {
    display: flex;
    align-items: center;
    gap: 1.2rem;
    margin-right: 2rem;

    .social img {
      width: 2rem;
      transition: transform 0.2s ease-in-out;

      &:hover {
        transform: scale(1.3);
      }
    }

    #socials {
      display: flex;
      align-items: center;
      background-color: #000;
      padding: 0.6em 1.4em;
      border-radius: 1.5rem;
      gap: 0.4rem;
      transition: all 200ms ease-in-out;
      margin-right: 0.6rem; // adds space from the right edge

      a {
        color: #F4EBD0;
        font-family: 'satoshi', sans-serif;
        font-weight: 500;
        text-decoration: none;
      }

      &:hover a {
        color: #FFB400;
      }

      img {
        width: 1.3rem;
        transition: transform 0.2s ease-in-out;
      }

      &:hover img {
        transform: translateX(4px);
      }
    }

    /* Hide entire right side on mobile */
    @media screen and (max-width: 1024px) {
      display: none !important;
    }
  }

  /* Hamburger */
  #menu-toggle {
    display: none;
    cursor: pointer;
    width: 40px;
    height: 30px;
    position: relative;
    right: 0;
    z-index: 13;

    span {
      display: block;
      width: 1.7rem;
      height: 2.5px;
      background-color: black;
      margin: 5px 0;
      transition: all 240ms ease-in-out;
    }

    &.active span:nth-child(1) {
      transform: rotate(45deg) translate(5px, 5px);
    }

    &.active span:nth-child(2) {
      opacity: 0;
    }

    &.active span:nth-child(3) {
      transform: rotate(-45deg) translate(5px, -5px);
    }

    @media screen and (max-width: 1024px) {
      display: block;
    }

    @media screen and (max-width: 375px) {
      width: 36px;
    }
  }

  /* Slide-over menu */
  #menu-links {
    position: fixed;
    top: 0;
    right: 0;
    height: 100%;
    width: min(260px, 85vw);
    background-color: #F4EBD0;
    box-shadow: -2px 0 5px rgba(0, 0, 0, 0.2);
    padding: 2rem 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
    transform: translateX(100%);
    will-change: transform;
    transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out;
    opacity: 0;
    pointer-events: none;
    z-index: 12;

    a {
      color: #000;
      font-family: 'satoshi', sans-serif;
      font-size: 18px;
      font-weight: 500;
      text-decoration: none;
    }

    #scmedia {
      display: flex;
      gap: 1rem;

      .social img {
        width: 2rem;
        transition: transform 0.2s ease-in-out;

        &:hover {
          transform: scale(1.2);
        }
      }
    }

    #join {
      display: flex;
      align-items: center;
      background-color: #000;
      padding: 0.6em 1.6em;
      border-radius: 1.7rem;
      gap: 0.4rem;
      cursor: pointer;
      transition: all 200ms ease-in-out;

      a {
        color: #F4EBD0;
      }

      img {
        width: 1.4rem;
      }

      &:hover img {
        transform: translateX(5px);
      }
    }

    &.active {
      transform: translateX(0);
      opacity: 1;
      pointer-events: auto;
    }
  }

  /* Responsive logo scaling */
  @media screen and (max-width: 600px) {
    height: 4rem;
    padding: 0.3rem 1rem;

    #logo img.logo-main,
    #logo img.logo-ut {
      height: 3.2rem;
    }

    #logo .divider {
      height: 3.2rem;
    }
  }

  @media screen and (max-width: 375px) {
    height: 3.5rem;
    padding: 0.25rem 0.85rem;

    #logo img.logo-main,
    #logo img.logo-ut {
      height: 2.6rem;
    }

    #logo .divider {
      height: 2.6rem;
    }
  }

  @media screen and (max-width: 340px) {
    height: 3.25rem;
    padding: 0.25rem 0.75rem;

    #logo img.logo-main,
    #logo img.logo-ut {
      height: 2.3rem;
    }

    #logo .divider {
      height: 2.3rem;
    }
  }
}

nav a.selected {
  color: #8A5900 !important;
  position: relative;
}
nav a.selected::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -6px;
  width: 18px;
  height: 2px;
  background: #FFB400;
  border-radius: 2px;
}
</style>