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
    <span
      class="neon-sign__backplate"
      aria-hidden="true"
    ></span>

    <p class="neon-sign__small">
      Welcome to
    </p>

    <h1 class="neon-sign__main">
      <span>Alco’s</span>
      <span>Bar</span>
    </h1>

    <span
      class="neon-sign__underline"
      aria-hidden="true"
    ></span>
  </div>
</template>

<style scoped lang="scss">
.neon-sign {
  position: relative;
  display: grid;
  justify-items: center;
  width: 100%;
  text-align: center;
  isolation: isolate;
}

.neon-sign::before {
  position: absolute;
  inset: -2rem -2.4rem -1.1rem;
  z-index: -2;
  content: '';
  background:
    radial-gradient(circle at 50% 48%, rgba(255, 59, 59, 0.22), transparent 58%),
    radial-gradient(circle at 50% 8%, rgba(255, 209, 102, 0.14), transparent 48%);
  filter: blur(13px);
  opacity: 0.98;
}

.neon-sign__backplate {
  position: absolute;
  inset: 4% 3% -5%;
  z-index: -1;
  background: radial-gradient(ellipse at center, rgba(9, 7, 6, 0.34), transparent 72%);
  border-radius: 50%;
}

.neon-sign__small {
  color: var(--color-neon-gold);
  font-family: var(--font-display);
  font-size: clamp(1.45rem, 3.4vw, 3.9rem);
  font-style: italic;
  letter-spacing: 0.02em;
  line-height: 0.9;
  opacity: 0;
  text-shadow:
    0 0 4px rgba(255, 209, 102, 0.95),
    0 0 14px rgba(255, 209, 102, 0.46),
    0 0 34px rgba(255, 209, 102, 0.22),
    0 7px 22px rgba(0, 0, 0, 0.6);
  animation: neonWarm 1.2s steps(1, end) 150ms forwards;
}

.neon-sign__main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.15em;
  margin-top: 0.03em;
  color: var(--color-neon-red);
  font-family: var(--font-display);
  font-size: clamp(3.1rem, 7.6vw, 8.25rem);
  font-weight: 800;
  letter-spacing: -0.08em;
  line-height: 0.82;
  opacity: 0;
  text-shadow:
    0 0 4px rgba(255, 59, 59, 0.95),
    0 0 13px rgba(255, 59, 59, 0.7),
    0 0 34px rgba(255, 59, 59, 0.36),
    0 0 70px rgba(255, 59, 59, 0.2),
    0 10px 26px rgba(0, 0, 0, 0.62);
  animation: neonRed 1.7s steps(1, end) 410ms forwards;
}

.neon-sign__underline {
  width: min(17rem, 72%);
  height: 0.16rem;
  margin-top: clamp(0.35rem, 0.9vw, 0.65rem);
  background: linear-gradient(90deg, transparent, rgba(255, 209, 102, 0.85), rgba(255, 59, 59, 0.72), transparent);
  border-radius: var(--radius-pill);
  box-shadow:
    0 0 10px rgba(255, 209, 102, 0.35),
    0 0 20px rgba(255, 59, 59, 0.18);
  opacity: 0;
  animation: neonLine 1.2s ease-out 720ms forwards;
}

.neon-sign--reduced .neon-sign__small,
.neon-sign--reduced .neon-sign__main,
.neon-sign--reduced .neon-sign__underline {
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

@keyframes neonLine {
  0% {
    opacity: 0;
    transform: scaleX(0.4);
  }

  100% {
    opacity: 0.86;
    transform: scaleX(1);
  }
}

@media (prefers-reduced-motion: reduce) {
  .neon-sign__small,
  .neon-sign__main,
  .neon-sign__underline {
    opacity: 1;
    animation: none;
  }
}

@media (max-width: 640px) {
  .neon-sign {
    justify-items: start;
    text-align: left;
  }

  .neon-sign__main {
    justify-content: flex-start;
  }

  .neon-sign__underline {
    width: min(13rem, 78%);
  }
}
</style>
