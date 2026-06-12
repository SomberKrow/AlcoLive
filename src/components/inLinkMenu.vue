<script setup>
defineProps({
  links: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <section
    id="link-menu"
    class="link-menu page-container"
    aria-labelledby="link-menu-title"
  >
    <div class="link-menu__panel">
      <div class="link-menu__header">
        <p>The Menu</p>

        <h2 id="link-menu-title">
          Pick your link.
        </h2>

        <span>
          Fast, readable, and phone-friendly. Same destinations, simpler reach.
        </span>
      </div>

      <ul
        class="link-menu__grid"
        aria-label="AlcoLive menu links"
      >
        <li
          v-for="link in links"
          :key="link.id"
          class="link-menu__item"
          :style="{ '--accent': link.accent }"
        >
          <a
            :href="link.url"
            target="_blank"
            rel="noreferrer noopener"
            :aria-label="`${link.label}: ${link.description}`"
          >
            <span class="link-menu__content">
              <small>{{ link.pour }}</small>
              <strong>{{ link.label }}</strong>
              <em>{{ link.description }}</em>
            </span>

            <span class="link-menu__action">
              Open
              <span aria-hidden="true">↗</span>
            </span>
          </a>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped lang="scss">
.link-menu {
  display: grid;
  padding-block: clamp(0.5rem, 2vw, 1.5rem) clamp(2.5rem, 5vw, 4rem);
}

.link-menu__panel {
  display: grid;
  gap: 1rem;
  padding: clamp(1rem, 2.4vw, 1.45rem);
  background:
    radial-gradient(circle at 50% 0%, rgba(255, 209, 102, 0.08), transparent 28rem),
    linear-gradient(180deg, rgba(246, 230, 200, 0.035), rgba(9, 7, 6, 0.18));
  border: 1px solid rgba(255, 209, 102, 0.1);
  border-radius: var(--radius-lg);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.035),
    0 22px 70px rgba(0, 0, 0, 0.22);
}

.link-menu__header {
  display: grid;
  justify-items: center;
  text-align: center;
}

.link-menu__header p {
  color: var(--color-neon-gold);
  font-family: var(--font-label);
  font-size: 0.7rem;
  font-weight: 950;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

.link-menu__header h2 {
  margin-top: 0.22rem;
  color: var(--color-cream);
  font-family: var(--font-display);
  font-size: clamp(1.7rem, 3.2vw, 2.65rem);
  letter-spacing: -0.045em;
  line-height: 1;
}

.link-menu__header span {
  max-width: 34rem;
  margin-top: 0.48rem;
  color: rgba(246, 230, 200, 0.62);
  font-size: 0.92rem;
  line-height: 1.45;
}

.link-menu__grid {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 0.75rem;
  padding: 0;
  margin: 0;
  list-style: none;
}

.link-menu__item a {
  position: relative;
  display: grid;
  min-height: 8.35rem;
  align-content: space-between;
  gap: 1rem;
  padding: 1rem;
  color: var(--color-cream);
  background:
    radial-gradient(circle at 50% 0%, color-mix(in srgb, var(--accent), transparent 82%), transparent 54%),
    linear-gradient(180deg, rgba(246, 230, 200, 0.045), rgba(9, 7, 6, 0.32));
  border: 1px solid color-mix(in srgb, var(--accent), transparent 72%);
  border-radius: var(--radius-md);
  box-shadow: 0 18px 34px rgba(0, 0, 0, 0.24);
  transition:
    transform var(--duration-fast) var(--ease-standard),
    border-color var(--duration-fast) var(--ease-standard),
    background-color var(--duration-fast) var(--ease-standard);
}

.link-menu__item a:hover,
.link-menu__item a:focus-visible {
  border-color: color-mix(in srgb, var(--accent), transparent 42%);
  transform: translateY(-0.12rem);
}

.link-menu__content {
  display: grid;
}

.link-menu__item small {
  color: color-mix(in srgb, var(--accent), var(--color-neon-gold) 24%);
  font-size: 0.62rem;
  font-weight: 950;
  letter-spacing: 0.15em;
  text-transform: uppercase;
}

.link-menu__item strong {
  display: block;
  margin-top: 0.22rem;
  font-family: var(--font-display);
  font-size: 1.35rem;
  letter-spacing: -0.04em;
  line-height: 1;
}

.link-menu__item em {
  margin-top: 0.75rem;
  color: rgba(246, 230, 200, 0.68);
  font-size: 0.82rem;
  font-style: normal;
  line-height: 1.38;
}

.link-menu__action {
  display: inline-flex;
  width: fit-content;
  align-items: center;
  gap: 0.35rem;
  padding: 0.4rem 0.58rem;
  color: color-mix(in srgb, var(--accent), var(--color-neon-gold) 20%);
  font-size: 0.72rem;
  font-weight: 900;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  background: rgba(9, 7, 6, 0.32);
  border: 1px solid color-mix(in srgb, var(--accent), transparent 72%);
  border-radius: var(--radius-pill);
}

@media (max-width: 1020px) {
  .link-menu {
    padding-top: 0.85rem;
  }

  .link-menu__grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 0.75rem;
  }

  .link-menu__item a {
    min-height: 7.4rem;
    padding: 0.95rem;
  }
}

@media (max-width: 560px) {
  .link-menu {
    padding-top: 0.25rem;
  }

  .link-menu__panel {
    margin-inline: -1rem;
    border-right: 0;
    border-left: 0;
    border-radius: 0;
  }

  .link-menu__header {
    justify-items: start;
    text-align: left;
  }

  .link-menu__grid {
    grid-template-columns: 1fr;
  }

  .link-menu__item a {
    min-height: auto;
  }
}
</style>
