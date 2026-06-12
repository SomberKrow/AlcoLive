<script setup>
defineProps({
  reducedMotion: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <div
    class="neon-sign"
    :class="{ 'neon-sign--reduced': reducedMotion }"
    aria-label="Welcome to Alco's Bar"
  >
    <p class="neon-sign__small">
      Welcome to
    </p>

    <h1 class="neon-sign__main">
      Alco’s Bar
    </h1>
  </div>
</template>

<style scoped lang="scss">
.neon-sign {
  position: relative;
  display: grid;
  justify-items: center;
  width: 100%;
  text-align: center;
}

.neon-sign::before {
  position: absolute;
  inset: -1.8rem -2rem -1rem;
  z-index: -1;
  content: '';
  background:
    radial-gradient(circle at 50% 42%, rgba(255, 59, 59, 0.18), transparent 58%),
    radial-gradient(circle at 50% 12%, rgba(255, 209, 102, 0.1), transparent 46%);
  filter: blur(12px);
  opacity: 0.96;
}

.neon-sign__small {
  color: var(--color-neon-gold);
  font-family: var(--font-display);
  font-size: clamp(1.55rem, 3.8vw, 4.2rem);
  font-style: italic;
  letter-spacing: 0.02em;
  line-height: 0.9;
  opacity: 0;
  text-shadow:
    0 0 5px rgba(255, 209, 102, 0.9),
    0 0 18px rgba(255, 209, 102, 0.38),
    0 0 42px rgba(255, 209, 102, 0.18);
  animation: neonWarm 1.2s steps(1, end) 150ms forwards;
}

.neon-sign__main {
  margin-top: 0.04em;
  color: var(--color-neon-red);
  font-family: var(--font-display);
  font-size: clamp(3.35rem, 8.2vw, 8.8rem);
  font-weight: 800;
  letter-spacing: -0.08em;
  line-height: 0.82;
  opacity: 0;
  text-shadow:
    0 0 5px rgba(255, 59, 59, 0.95),
    0 0 16px rgba(255, 59, 59, 0.58),
    0 0 42px rgba(255, 59, 59, 0.3),
    0 9px 24px rgba(0, 0, 0, 0.56);
  animation: neonRed 1.7s steps(1, end) 410ms forwards;
}

.neon-sign--reduced .neon-sign__small,
.neon-sign--reduced .neon-sign__main {
  opacity: 1;
  animation: none;
}

@keyframes neonWarm {
  0%,
  16%,
  30% {
    opacity: 0.22;
  }

  17%,
  29%,
  100% {
    opacity: 1;
  }
}

@keyframes neonRed {
  0%,
  12%,
  24%,
  38% {
    opacity: 0.12;
  }

  13%,
  23%,
  39%,
  100% {
    opacity: 1;
  }
}

@media (prefers-reduced-motion: reduce) {
  .neon-sign__small,
  .neon-sign__main {
    opacity: 1;
    animation: none;
  }
}

@media (max-width: 640px) {
  .neon-sign {
    justify-items: start;
    text-align: left;
  }
}
</style>
