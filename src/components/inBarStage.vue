<script setup>
import InBottleCard from './inBottleCard.vue'
import InNeonSign from './inNeonSign.vue'

defineProps({
  links: {
    type: Array,
    required: true
  },
  reducedMotion: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <section
    id="top"
    class="bar-stage page-container"
    aria-labelledby="bar-stage-title"
  >
    <div class="bar-stage__scene">
      <span
        class="bar-stage__ambient"
        aria-hidden="true"
      ></span>

      <div class="bar-stage__sign-area">
        <InNeonSign :reduced-motion="reducedMotion" />

        <div class="bar-stage__copy">
          <h2 id="bar-stage-title">
            Pull up a seat. Pick your pour.
          </h2>

          <p>
            Streams, clips, posts, and mocktails welcome.
          </p>

          <a
            class="bar-stage__menu-jump"
            href="#link-menu"
          >
            Open The Menu
          </a>
        </div>
      </div>

      <div
        id="bottle-links"
        class="bar-stage__bottles"
      >
        <p class="bar-stage__eyebrow">
          Choose a Bottle
        </p>

        <ul
          class="bar-stage__list"
          aria-label="AlcoLive bottle links"
        >
          <InBottleCard
            v-for="(link, index) in links"
            :key="link.id"
            :link="link"
            :index="index"
            :reduced-motion="reducedMotion"
          />
        </ul>
      </div>

      <span
        class="bar-stage__bottle-glow"
        aria-hidden="true"
      ></span>

      <span
        class="bar-stage__counter-line"
        aria-hidden="true"
      ></span>
    </div>
  </section>
</template>

<style scoped lang="scss">
.bar-stage {
  padding-block: clamp(0.9rem, 2vw, 1.65rem) clamp(2.2rem, 5vw, 4rem);
}

.bar-stage__scene {
  position: relative;
  min-height: min(56.25vw, 810px);
  overflow: hidden;
  aspect-ratio: 16 / 9;
  background:
    linear-gradient(180deg, rgba(9, 7, 6, 0.02), rgba(9, 7, 6, 0.08)),
    url('/assets/bar/alcos-bar-stage.webp') center / cover no-repeat;
  background-color: #100906;
  border: 1px solid rgba(255, 209, 102, 0.12);
  border-radius: calc(var(--radius-lg) + 0.3rem);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    inset 0 -68px 110px rgba(0, 0, 0, 0.44),
    0 36px 96px rgba(0, 0, 0, 0.42);
  isolation: isolate;
}

.bar-stage__scene::before {
  position: absolute;
  inset: 0;
  z-index: 1;
  pointer-events: none;
  content: '';
  background:
    radial-gradient(ellipse at 50% 18%, rgba(255, 209, 102, 0.09), transparent 33%),
    radial-gradient(ellipse at 50% 55%, transparent 0 40%, rgba(9, 7, 6, 0.18) 72%),
    linear-gradient(90deg, rgba(0, 0, 0, 0.2), transparent 18%, transparent 82%, rgba(0, 0, 0, 0.2));
}

.bar-stage__scene::after {
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 3;
  height: 28%;
  pointer-events: none;
  content: '';
  background: linear-gradient(180deg, transparent, rgba(5, 4, 3, 0.54));
}

.bar-stage__ambient {
  position: absolute;
  inset: 0;
  z-index: 2;
  pointer-events: none;
  background:
    radial-gradient(circle at 50% 12%, rgba(255, 59, 59, 0.08), transparent 24rem),
    radial-gradient(ellipse at 50% 71%, rgba(255, 174, 78, 0.16), transparent 28%);
  mix-blend-mode: screen;
  opacity: 0.76;
}

.bar-stage__sign-area {
  position: absolute;
  top: 6.2%;
  right: 25%;
  left: 25%;
  z-index: 7;
  display: grid;
  justify-items: center;
  padding: clamp(0.45rem, 0.9vw, 0.85rem) clamp(0.75rem, 1.5vw, 1.4rem);
  text-align: center;
}

.bar-stage__sign-area::before {
  position: absolute;
  inset: 4% 0 -8%;
  z-index: -1;
  content: '';
  background:
    radial-gradient(ellipse at 50% 22%, rgba(9, 7, 6, 0.5), transparent 70%),
    linear-gradient(180deg, rgba(9, 7, 6, 0.26), rgba(9, 7, 6, 0.08));
  border: 1px solid rgba(255, 209, 102, 0.045);
  border-radius: var(--radius-lg);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.035),
    0 18px 60px rgba(0, 0, 0, 0.22);
  opacity: 0.7;
}

.bar-stage__copy {
  display: grid;
  justify-items: center;
  max-width: 580px;
  margin-top: clamp(0.16rem, 0.45vw, 0.42rem);
}

.bar-stage__copy h2 {
  color: var(--color-cream);
  font-family: var(--font-display);
  font-size: clamp(1.35rem, 2.45vw, 2.55rem);
  letter-spacing: -0.045em;
  line-height: 1;
  text-shadow: 0 7px 18px rgba(0, 0, 0, 0.48);
}

.bar-stage__copy p {
  max-width: 420px;
  margin-top: 0.42rem;
  color: rgba(246, 230, 200, 0.76);
  font-size: clamp(0.82rem, 1.1vw, 1rem);
  line-height: 1.5;
  text-shadow: 0 5px 14px rgba(0, 0, 0, 0.5);
}

.bar-stage__menu-jump {
  display: none;
  margin-top: 1rem;
  padding: 0.72rem 0.95rem;
  color: var(--color-cream);
  font-size: 0.78rem;
  font-weight: 950;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  background: rgba(9, 7, 6, 0.62);
  border: 1px solid rgba(255, 209, 102, 0.26);
  border-radius: var(--radius-pill);
  box-shadow:
    0 0 18px rgba(255, 59, 59, 0.14),
    0 16px 34px rgba(0, 0, 0, 0.32);
  transition:
    transform var(--duration-fast) var(--ease-standard),
    border-color var(--duration-fast) var(--ease-standard),
    background-color var(--duration-fast) var(--ease-standard);
}

.bar-stage__menu-jump:hover,
.bar-stage__menu-jump:focus-visible {
  background: rgba(255, 209, 102, 0.08);
  border-color: rgba(255, 209, 102, 0.5);
  transform: translateY(-0.1rem);
}

.bar-stage__bottles {
  position: absolute;
  right: 12%;
  bottom: 12.5%;
  left: 12%;
  z-index: 8;
  display: grid;
  gap: 0.48rem;
  justify-items: center;
}

.bar-stage__eyebrow {
  color: var(--color-neon-gold);
  font-family: var(--font-label);
  font-size: clamp(0.58rem, 0.82vw, 0.72rem);
  font-weight: 950;
  letter-spacing: 0.2em;
  line-height: 1;
  text-transform: uppercase;
  text-shadow:
    0 0 8px rgba(255, 209, 102, 0.56),
    0 4px 12px rgba(0, 0, 0, 0.5);
}

.bar-stage__list {
  display: flex;
  width: 100%;
  align-items: flex-end;
  justify-content: center;
  gap: clamp(0.15rem, 0.9vw, 0.76rem);
  padding: 0;
  margin: 0;
  list-style: none;
}

.bar-stage__bottle-glow {
  position: absolute;
  right: 8%;
  bottom: 14.2%;
  left: 8%;
  z-index: 5;
  height: 2.7rem;
  pointer-events: none;
  background: radial-gradient(ellipse at center, rgba(255, 163, 78, 0.35), transparent 68%);
  filter: blur(14px);
  opacity: 0.82;
}

.bar-stage__counter-line {
  position: absolute;
  right: 7%;
  bottom: 13.6%;
  left: 7%;
  z-index: 6;
  height: 0.16rem;
  pointer-events: none;
  background: linear-gradient(90deg, transparent, rgba(255, 209, 102, 0.52), rgba(255, 90, 45, 0.44), transparent);
  border-radius: var(--radius-pill);
  filter: blur(1px);
  opacity: 0.72;
}

@media (max-width: 1180px) {
  .bar-stage__sign-area {
    right: 20%;
    left: 20%;
  }

  .bar-stage__bottles {
    right: 8%;
    left: 8%;
  }
}

@media (max-width: 1020px) {
  .bar-stage {
    padding-block: 0.85rem 1.25rem;
  }

  .bar-stage__scene {
    min-height: clamp(25rem, 58vw, 34rem);
    aspect-ratio: auto;
    background-position: center;
    background-size: cover;
    border-radius: var(--radius-lg);
  }

  .bar-stage__scene::before {
    background:
      radial-gradient(ellipse at 50% 22%, rgba(255, 209, 102, 0.12), transparent 34%),
      linear-gradient(180deg, rgba(5, 4, 3, 0.12), rgba(5, 4, 3, 0.5)),
      linear-gradient(90deg, rgba(0, 0, 0, 0.24), transparent 24%, transparent 76%, rgba(0, 0, 0, 0.24));
  }

  .bar-stage__scene::after,
  .bar-stage__bottles,
  .bar-stage__bottle-glow,
  .bar-stage__counter-line {
    display: none;
  }

  .bar-stage__sign-area {
    top: 50%;
    right: clamp(1rem, 4vw, 2rem);
    left: clamp(1rem, 4vw, 2rem);
    transform: translateY(-50%);
  }

  .bar-stage__copy {
    max-width: 36rem;
  }

  .bar-stage__menu-jump {
    display: inline-flex;
  }
}

@media (max-width: 640px) {
  .bar-stage {
    padding-top: 0.65rem;
  }

  .bar-stage__scene {
    min-height: 25.5rem;
    margin-inline: -1rem;
    border-right: 0;
    border-left: 0;
    border-radius: 0;
  }

  .bar-stage__sign-area,
  .bar-stage__copy {
    justify-items: start;
    text-align: left;
  }

  .bar-stage__sign-area::before {
    inset: -3% -0.6rem -10%;
  }

  .bar-stage__copy h2 {
    font-size: clamp(1.45rem, 9vw, 2.35rem);
  }

  .bar-stage__copy p {
    max-width: 20rem;
  }
}
</style>
