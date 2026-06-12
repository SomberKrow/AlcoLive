<script setup>
import { computed } from 'vue'

const props = defineProps({
  link: {
    type: Object,
    required: true
  },
  index: {
    type: Number,
    default: 0
  },
  reducedMotion: {
    type: Boolean,
    default: false
  }
})

const tilt = computed(() => {
  const values = ['-0.75deg', '0.58deg', '-0.32deg', '0.68deg', '-0.46deg']

  return values[props.index % values.length]
})

const bottleStyles = computed(() => ({
  '--accent': props.link.accent,
  '--tilt': tilt.value,
  '--stagger': `${0.58 + props.index * 0.08}s`,
  '--idle-delay': `${props.index * 0.42}s`
}))

const ariaLabel = computed(() => `${props.link.label}: ${props.link.description}`)
</script>

<template>
  <li
    class="bottle-card"
    :class="{ 'bottle-card--reduced': reducedMotion }"
    :style="bottleStyles"
  >
    <a
      class="bottle-card__link"
      :href="link.url"
      target="_blank"
      rel="noreferrer noopener"
      :aria-label="ariaLabel"
    >
      <span
        class="bottle-card__light"
        aria-hidden="true"
      ></span>

      <span class="bottle-card__image-frame">
        <img
          class="bottle-card__image"
          :src="link.image"
          :alt="`${link.label} bottle`"
          width="1000"
          height="1400"
          draggable="false"
          decoding="async"
        />
      </span>

      <span
        class="bottle-card__hover-card"
        aria-hidden="true"
      >
        <small>{{ link.pour }}</small>
        <strong>{{ link.label }}</strong>
        <span>{{ link.description }}</span>
      </span>
    </a>
  </li>
</template>

<style scoped lang="scss">
.bottle-card {
  --bottle-width: clamp(6.9rem, 8vw, 9.2rem);
  --bottle-height: clamp(12.9rem, 16.8vw, 18.4rem);

  position: relative;
  flex: 0 0 auto;
  width: calc(var(--bottle-width) + 0.2rem);
  min-height: calc(var(--bottle-height) + 0.4rem);
  scroll-snap-align: center;
}

.bottle-card__link {
  position: relative;
  display: grid;
  min-height: calc(var(--bottle-height) + 0.4rem);
  place-items: end center;
  isolation: isolate;
}

.bottle-card__light {
  position: absolute;
  right: 0.6rem;
  bottom: 0.14rem;
  left: 0.6rem;
  z-index: -1;
  height: 42%;
  background: radial-gradient(
    ellipse at 50% 74%,
    color-mix(in srgb, var(--accent), transparent 58%),
    transparent 72%
  );
  filter: blur(18px);
  opacity: 0.2;
  transform: scale(0.9);
  animation: bottleIdle 5.8s ease-in-out var(--idle-delay) infinite;
  transition:
    opacity var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-standard);
}

.bottle-card__image-frame {
  position: relative;
  display: grid;
  width: var(--bottle-width);
  height: var(--bottle-height);
  place-items: end center;
  opacity: 0;
  transform: translateY(0.85rem) rotate(var(--tilt)) scale(0.97);
  transform-origin: 50% 96%;
  filter:
    drop-shadow(0 1.1rem 0.72rem rgba(0, 0, 0, 0.52))
    drop-shadow(0 0 0.4rem color-mix(in srgb, var(--accent), transparent 90%));
  animation: bottleSettle 620ms var(--ease-bounce) var(--stagger) forwards;
  transition:
    filter var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-bounce);
}

.bottle-card__image-frame::after {
  position: absolute;
  right: 22%;
  bottom: 0.34rem;
  left: 22%;
  z-index: 1;
  height: 0.52rem;
  content: '';
  background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.62), transparent 74%);
  filter: blur(5px);
  opacity: 0.82;
}

.bottle-card__image {
  position: relative;
  z-index: 2;
  display: block;
  width: 100%;
  height: 100%;
  object-fit: contain;
  object-position: center bottom;
  pointer-events: none;
  user-select: none;
}

.bottle-card__hover-card {
  position: absolute;
  bottom: calc(100% + 0.12rem);
  left: 50%;
  z-index: 20;
  display: grid;
  width: min(14rem, 78vw);
  gap: 0.2rem;
  padding: 0.75rem 0.85rem;
  pointer-events: none;
  background: rgba(9, 7, 6, 0.9);
  border: 1px solid color-mix(in srgb, var(--accent), transparent 48%);
  border-radius: var(--radius-md);
  box-shadow:
    0 18px 38px rgba(0, 0, 0, 0.42),
    0 0 18px color-mix(in srgb, var(--accent), transparent 78%);
  opacity: 0;
  transform: translate(-50%, 0.7rem) scale(0.96);
  transition:
    opacity var(--duration-fast) var(--ease-standard),
    transform var(--duration-fast) var(--ease-standard);
}

.bottle-card__hover-card small {
  color: color-mix(in srgb, var(--accent), var(--color-neon-gold) 28%);
  font-size: 0.62rem;
  font-weight: 950;
  letter-spacing: 0.16em;
  line-height: 1;
  text-transform: uppercase;
}

.bottle-card__hover-card strong {
  color: var(--color-cream);
  font-family: var(--font-display);
  font-size: 1.18rem;
  letter-spacing: -0.04em;
  line-height: 1;
}

.bottle-card__hover-card span {
  color: rgba(246, 230, 200, 0.72);
  font-size: 0.78rem;
  line-height: 1.38;
}

.bottle-card__link:hover .bottle-card__image-frame,
.bottle-card__link:focus-visible .bottle-card__image-frame {
  filter:
    drop-shadow(0 1.35rem 0.95rem rgba(0, 0, 0, 0.6))
    drop-shadow(0 0 0.95rem color-mix(in srgb, var(--accent), transparent 74%));
  transform: translateY(-0.22rem) rotate(0deg) scale(1.022);
}

.bottle-card__link:hover .bottle-card__light,
.bottle-card__link:focus-visible .bottle-card__light {
  opacity: 0.48;
  transform: scale(1.05);
}

.bottle-card__link:hover .bottle-card__hover-card,
.bottle-card__link:focus-visible .bottle-card__hover-card {
  opacity: 1;
  transform: translate(-50%, 0) scale(1);
}

.bottle-card--reduced .bottle-card__image-frame {
  opacity: 1;
  animation: none;
  transform: rotate(var(--tilt));
}

.bottle-card--reduced .bottle-card__light {
  animation: none;
}

@keyframes bottleSettle {
  0% {
    opacity: 0;
    transform: translateY(0.85rem) rotate(var(--tilt)) scale(0.97);
  }

  100% {
    opacity: 1;
    transform: translateY(0) rotate(var(--tilt)) scale(1);
  }
}

@keyframes bottleIdle {
  0%,
  100% {
    opacity: 0.16;
    transform: scale(0.9);
  }

  50% {
    opacity: 0.28;
    transform: scale(0.98);
  }
}

@media (prefers-reduced-motion: reduce) {
  .bottle-card__image-frame {
    opacity: 1;
    animation: none;
    transform: rotate(var(--tilt));
  }

  .bottle-card__light {
    animation: none;
  }

  .bottle-card__link:hover .bottle-card__image-frame,
  .bottle-card__link:focus-visible .bottle-card__image-frame {
    transform: rotate(var(--tilt));
  }
}

@media (max-width: 1020px) {
  .bottle-card {
    --bottle-width: 7.25rem;
    --bottle-height: 15.4rem;
  }

  .bottle-card__hover-card {
    display: none;
  }
}
</style>
