<script setup>
defineProps({
  links: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <footer class="app-footer">
    <div class="app-footer__inner page-container">
      <p>
        Alco’s Bar · Bar Open Alpha
      </p>

      <nav
        class="app-footer__links"
        aria-label="Footer social links"
      >
        <a
          v-for="link in links"
          :key="link.id"
          :href="link.url"
          target="_blank"
          rel="noreferrer noopener"
        >
          {{ link.label }}
        </a>
      </nav>

      <p class="app-footer__note">
        Drinks, mocktails, and good company.
      </p>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.app-footer {
  padding-block: 1.25rem;
  border-top: 1px solid rgba(255, 209, 102, 0.08);
  background:
    linear-gradient(180deg, rgba(9, 7, 6, 0.78), rgba(5, 4, 3, 0.92));
}

.app-footer__inner {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  gap: 1rem;
}

.app-footer p {
  color: rgba(246, 230, 200, 0.46);
  font-size: 0.8rem;
}

.app-footer__links {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.35rem 0.7rem;
}

.app-footer__links a {
  color: rgba(246, 230, 200, 0.58);
  font-size: 0.82rem;
  font-weight: 850;
  transition: color var(--duration-fast) var(--ease-standard);
}

.app-footer__links a:hover,
.app-footer__links a:focus-visible {
  color: var(--color-neon-gold);
}

.app-footer__note {
  justify-self: end;
}

@media (max-width: 800px) {
  .app-footer__inner {
    grid-template-columns: 1fr;
    justify-items: start;
  }

  .app-footer__links {
    justify-content: flex-start;
  }

  .app-footer__note {
    justify-self: start;
  }
}
</style>
