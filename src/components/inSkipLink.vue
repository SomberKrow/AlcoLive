<template>
  <a
    class="skip-link"
    href="#main-content"
  >
    Skip to content
  </a>
</template>

<style scoped lang="scss">
.skip-link {
  position: fixed;
  top: 0.75rem;
  left: 0.75rem;
  z-index: 100;
  padding: 0.7rem 0.9rem;
  color: var(--color-bar-black);
  font-weight: 900;
  background: var(--color-neon-gold);
  border-radius: var(--radius-pill);
  transform: translateY(-180%);
  transition: transform var(--duration-fast) var(--ease-standard);
}

.skip-link:focus-visible {
  transform: translateY(0);
}
</style>
