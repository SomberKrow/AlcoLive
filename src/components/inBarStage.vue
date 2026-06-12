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
      <div class="bar-stage__sign-area">
        <InNeonSign :reduced-motion="reducedMotion" />

        <div class="bar-stage__copy">
          <h2 id="bar-stage-title">
            Pull up a seat. Pick your pour.
          </h2>

          <p>
            Streams, clips, posts, and mocktails welcome.
          </p>

          <p class="bar-stage__mobile-cue">
            The bottle shelf stays behind the bar on desktop. On smaller screens, use the menu below.
          </p>
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
          aria-label="AlcoLive social links"
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
    </div>
  </section>
</template>

<style scoped lang="scss">
.bar-stage {
  padding-block: clamp(1rem, 2vw, 1.65rem) clamp(2.2rem, 5vw, 4rem);
}

.bar-stage__scene {
  position: relative;
  overflow: hidden;
  min-height: min(56.25vw, 810px);
  aspect-ratio: 16 / 9;
  background:
    linear-gradient(180deg, rgba(9, 7, 6, 0.02), rgba(9, 7, 6, 0.08)),
    url('/assets/bar/alcos-bar-stage.webp') center / cover no-repeat;
  border: 1px solid rgba(255, 209, 102, 0.12);
  border-radius: calc(var(--radius-lg) + 0.3rem);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    inset 0 -60px 100px rgba(0, 0, 0, 0.42),
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
    radial-gradient(ellipse at 50% 22%, rgba(255, 209, 102, 0.08), transparent 34%),
    radial-gradient(ellipse at 50% 54%, transparent 0 42%, rgba(9, 7, 6, 0.16) 70%),
    linear-gradient(90deg, rgba(0, 0, 0, 0.18), transparent 18%, transparent 82%, rgba(0, 0, 0, 0.18));
}

.bar-stage__scene::after {
  position: absolute;
  right: 9%;
  bottom: 18.2%;
  left: 9%;
  z-index: 2;
  height: 1.7rem;
  pointer-events: none;
  content: '';
  background: radial-gradient(ellipse at center, rgba(255, 155, 60, 0.34), transparent 66%);
  filter: blur(11px);
  opacity: 0.78;
}

.bar-stage__sign-area {
  position: absolute;
  top: 7%;
  right: 28%;
  left: 28%;
  z-index: 5;
  display: grid;
  justify-items: center;
  text-align: center;
}

.bar-stage__copy {
  display: grid;
  justify-items: center;
  max-width: 580px;
  margin-top: clamp(0.25rem, 0.7vw, 0.6rem);
}

.bar-stage__copy h2 {
  color: var(--color-cream);
  font-family: var(--font-display);
  font-size: clamp(1.4rem, 2.6vw, 2.7rem);
  letter-spacing: -0.045em;
  line-height: 1;
  text-shadow: 0 7px 18px rgba(0, 0, 0, 0.42);
}

.bar-stage__copy p {
  max-width: 420px;
  margin-top: 0.45rem;
  color: rgba(246, 230, 200, 0.74);
  font-size: clamp(0.82rem, 1.15vw, 1rem);
  line-height: 1.5;
  text-shadow: 0 5px 14px rgba(0, 0, 0, 0.42);
}

.bar-stage__mobile-cue {
  display: none;
}

.bar-stage__bottles {
  position: absolute;
  right: 12%;
  bottom: 14.1%;
  left: 12%;
  z-index: 6;
  display: grid;
  gap: 0.55rem;
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
  align-items: flex-end;
  justify-content: center;
  width: 100%;
  gap: clamp(0.2rem, 0.95vw, 0.8rem);
  padding: 0;
  margin: 0;
  list-style: none;
}

@media (max-width: 1020px) {
  .bar-stage {
    padding-block: 0.9rem 1.25rem;
  }

  .bar-stage__scene {
    min-height: clamp(24rem, 58vw, 34rem);
    aspect-ratio: auto;
    background-position: center;
    background-size: cover;
    border-radius: var(--radius-lg);
  }

  .bar-stage__scene::before {
    background:
      radial-gradient(ellipse at 50% 22%, rgba(255, 209, 102, 0.12), transparent 34%),
      linear-gradient(180deg, rgba(5, 4, 3, 0.12), rgba(5, 4, 3, 0.48)),
      linear-gradient(90deg, rgba(0, 0, 0, 0.24), transparent 24%, transparent 76%, rgba(0, 0, 0, 0.24));
  }

  .bar-stage__scene::after {
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

  .bar-stage__mobile-cue {
    display: block;
    max-width: 31rem;
    margin-top: 0.9rem;
    color: rgba(246, 230, 200, 0.58);
    font-size: 0.82rem;
  }

  .bar-stage__bottles {
    display: none;
  }
}

@media (max-width: 640px) {
  .bar-stage {
    padding-top: 0.7rem;
  }

  .bar-stage__scene {
    min-height: 26rem;
    margin-inline: -1rem;
    border-right: 0;
    border-left: 0;
    border-radius: 0;
  }

  .bar-stage__sign-area {
    justify-items: start;
    text-align: left;
  }

  .bar-stage__copy {
    justify-items: start;
  }
}
</style>
