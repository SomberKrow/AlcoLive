<template>
  <header
    class="site-header"
    aria-label="AlcoLive site header"
  >
    <div class="site-header__inner page-container">
      <a
        class="site-header__brand"
        href="#top"
        aria-label="Back to the top of Alco’s Bar"
      >
        <span
          class="site-header__mark"
          aria-hidden="true"
        >
          <svg
            viewBox="0 0 24 24"
            focusable="false"
          >
            <path
              d="M5 3h14l-5.2 7.2v6.2l3.8 2.2v1.4H6.4v-1.4l3.8-2.2v-6.2L5 3Zm3.4 2 3.6 4.9L15.6 5H8.4Z"
              fill="currentColor"
            />
          </svg>
        </span>

        <span class="site-header__text">
          <strong>Alco’s Bar</strong>
          <small>Creator link shelf</small>
        </span>
      </a>

      <nav
        class="site-header__nav"
        aria-label="Page navigation"
      >
        <a href="#top">Bar</a>
        <a href="#link-menu">Menu</a>
      </nav>
    </div>
  </header>
</template>

<style scoped lang="scss">
.site-header {
  position: sticky;
  top: 0;
  z-index: 40;
  min-height: var(--header-height);
  border-bottom: 1px solid rgba(255, 209, 102, 0.09);
  background:
    linear-gradient(180deg, rgba(9, 7, 6, 0.92), rgba(9, 7, 6, 0.76));
  backdrop-filter: blur(18px);
}

.site-header__inner {
  display: flex;
  min-height: var(--header-height);
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.site-header__brand {
  display: inline-flex;
  align-items: center;
  gap: 0.72rem;
  color: var(--color-cream);
}

.site-header__mark {
  display: grid;
  width: 2.2rem;
  height: 2.2rem;
  place-items: center;
  color: var(--color-neon-red);
  background: rgba(255, 59, 59, 0.045);
  border: 1px solid rgba(255, 59, 59, 0.24);
  border-radius: 50%;
  box-shadow: 0 0 18px rgba(255, 59, 59, 0.14);
}

.site-header__mark svg {
  width: 1.08rem;
  height: 1.08rem;
}

.site-header__text {
  display: grid;
  gap: 0.04rem;
}

.site-header__text strong {
  font-family: var(--font-display);
  font-size: 1.16rem;
  letter-spacing: -0.035em;
  line-height: 1;
}

.site-header__text small {
  color: rgba(246, 230, 200, 0.52);
  font-size: 0.64rem;
  font-weight: 850;
  letter-spacing: 0.12em;
  line-height: 1;
  text-transform: uppercase;
}

.site-header__nav {
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
}

.site-header__nav a {
  padding: 0.52rem 0.72rem;
  color: rgba(246, 230, 200, 0.68);
  font-size: 0.76rem;
  font-weight: 900;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border-radius: var(--radius-pill);
  transition:
    color var(--duration-fast) var(--ease-standard),
    background-color var(--duration-fast) var(--ease-standard);
}

.site-header__nav a:hover,
.site-header__nav a:focus-visible {
  color: var(--color-neon-gold);
  background: rgba(255, 209, 102, 0.075);
}

@media (max-width: 640px) {
  .site-header__text small {
    display: none;
  }

  .site-header__nav a {
    padding-inline: 0.46rem;
    font-size: 0.68rem;
  }
}
</style>
