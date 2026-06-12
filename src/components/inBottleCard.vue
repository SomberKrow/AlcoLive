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
  const values = ['-0.8deg', '0.55deg', '-0.28deg', '0.72deg', '-0.48deg']

  return values[props.index % values.length]
})

const bottleStyles = computed(() => ({
  '--accent': props.link.accent,
  '--tilt': tilt.value,
  '--stagger': `${0.5 + props.index * 0.08}s`,
  '--idle-delay': `${props.index * 0.42}s`
}))

const ariaLabel = computed(() => `${props.link.label}: ${props.link.description}`)

function handlePointerMove(event) {
  if (props.reducedMotion) return

  const target = event.currentTarget
  const rect = target.getBoundingClientRect()
  const x = ((event.clientX - rect.left) / rect.width) * 100
  const y = ((event.clientY - rect.top) / rect.height) * 100
  const rotateY = ((x - 50) / 50) * 5
  const rotateX = ((50 - y) / 50) * 3.5

  target.style.setProperty('--mx', `${x.toFixed(2)}%`)
  target.style.setProperty('--my', `${y.toFixed(2)}%`)
  target.style.setProperty('--rx', `${rotateX.toFixed(2)}deg`)
  target.style.setProperty('--ry', `${rotateY.toFixed(2)}deg`)
}

function resetPointer(event) {
  const target = event.currentTarget

  target.style.setProperty('--mx', '50%')
  target.style.setProperty('--my', '42%')
  target.style.setProperty('--rx', '0deg')
  target.style.setProperty('--ry', '0deg')
}
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
      @pointermove="handlePointerMove"
      @pointerleave="resetPointer"
      @blur="resetPointer"
    >
      <span
        class="bottle-card__light"
        aria-hidden="true"
      ></span>

      <span class="bottle-card__image-frame">
        <span
          class="bottle-card__shine"
          aria-hidden="true"
        ></span>

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
  --bottle-width: clamp(6.95rem, 8vw, 9.25rem);
  --bottle-height: clamp(12.95rem, 16.8vw, 18.55rem);
  --mx: 50%;
  --my: 42%;
  --rx: 0deg;
  --ry: 0deg;

  position: relative;
  flex: 0 0 auto;
  width: calc(var(--bottle-width) + 0.3rem);
  min-height: calc(var(--bottle-height) + 0.5rem);
  perspective: 900px;
  scroll-snap-align: center;
}

.bottle-card__link {
  position: relative;
  display: grid;
  min-height: calc(var(--bottle-height) + 0.5rem);
  place-items: end center;
  isolation: isolate;
}

.bottle-card__link:focus-visible {
  outline-offset: 0.45rem;
}

.bottle-card__light {
  position: absolute;
  right: 0.45rem;
  bottom: -0.1rem;
  left: 0.45rem;
  z-index: -1;
  height: 46%;
  background: radial-gradient(
    ellipse at 50% 76%,
    color-mix(in srgb, var(--accent), transparent 55%),
    transparent 72%
  );
  filter: blur(18px);
  opacity: 0.22;
  transform: scale(0.9);
  animation: bottleIdle 5.8s ease-in-out var(--idle-delay) infinite;
  transition:
    opacity var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-standard),
    filter var(--duration-medium) var(--ease-standard);
}

.bottle-card__image-frame {
  position: relative;
  display: grid;
  width: var(--bottle-width);
  height: var(--bottle-height);
  place-items: end center;
  opacity: 0;
  transform:
    translateY(0.85rem)
    rotate(var(--tilt))
    rotateX(0deg)
    rotateY(0deg)
    scale(0.97);
  transform-origin: 50% 96%;
  transform-style: preserve-3d;
  filter:
    drop-shadow(0 1.05rem 0.7rem rgba(0, 0, 0, 0.54))
    drop-shadow(0 0 0.42rem color-mix(in srgb, var(--accent), transparent 90%));
  animation: bottleSettle 620ms var(--ease-bounce) var(--stagger) forwards;
  transition:
    filter var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-bounce);
  will-change: transform, filter;
}

.bottle-card__image-frame::before {
  position: absolute;
  right: 18%;
  bottom: 0.12rem;
  left: 18%;
  z-index: 1;
  height: 0.64rem;
  content: '';
  background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.68), transparent 74%);
  filter: blur(5px);
  opacity: 0.86;
  transform: translateZ(-1px) scaleX(0.92);
  transition:
    opacity var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-standard);
}

.bottle-card__image-frame::after {
  position: absolute;
  right: 14%;
  bottom: -0.18rem;
  left: 14%;
  z-index: 0;
  height: 1.3rem;
  content: '';
  background: radial-gradient(
    ellipse at center,
    color-mix(in srgb, var(--accent), transparent 76%),
    transparent 68%
  );
  filter: blur(7px);
  opacity: 0.42;
  transform: scaleX(0.88);
  transition:
    opacity var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-standard);
}

.bottle-card__shine {
  position: absolute;
  inset: 0;
  z-index: 3;
  pointer-events: none;
  background:
    radial-gradient(circle at var(--mx) var(--my), rgba(255, 255, 255, 0.2), transparent 18%),
    linear-gradient(105deg, transparent 30%, rgba(255, 255, 255, 0.13), transparent 48%);
  mix-blend-mode: screen;
  opacity: 0;
  transform: translateZ(32px);
  transition: opacity var(--duration-medium) var(--ease-standard);
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
  transform: translateZ(22px);
}

.bottle-card__hover-card {
  position: absolute;
  bottom: calc(100% + 0.18rem);
  left: 50%;
  z-index: 20;
  display: grid;
  width: min(14rem, 78vw);
  gap: 0.2rem;
  padding: 0.75rem 0.85rem;
  pointer-events: none;
  background:
    radial-gradient(circle at 50% 0%, color-mix(in srgb, var(--accent), transparent 86%), transparent 54%),
    rgba(9, 7, 6, 0.92);
  border: 1px solid color-mix(in srgb, var(--accent), transparent 48%);
  border-radius: var(--radius-md);
  box-shadow:
    0 18px 38px rgba(0, 0, 0, 0.44),
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
  color: rgba(246, 230, 200, 0.74);
  font-size: 0.78rem;
  line-height: 1.38;
}

.bottle-card__link:hover .bottle-card__image-frame,
.bottle-card__link:focus-visible .bottle-card__image-frame {
  filter:
    drop-shadow(0 1.3rem 0.95rem rgba(0, 0, 0, 0.62))
    drop-shadow(0 0 0.95rem color-mix(in srgb, var(--accent), transparent 72%));
  transform:
    translateY(-0.28rem)
    rotate(0deg)
    rotateX(var(--rx))
    rotateY(var(--ry))
    scale(1.026);
}

.bottle-card__link:hover .bottle-card__image-frame::before,
.bottle-card__link:focus-visible .bottle-card__image-frame::before {
  opacity: 0.7;
  transform: translateZ(-1px) scaleX(1.04);
}

.bottle-card__link:hover .bottle-card__image-frame::after,
.bottle-card__link:focus-visible .bottle-card__image-frame::after {
  opacity: 0.68;
  transform: scaleX(1.1);
}

.bottle-card__link:hover .bottle-card__shine,
.bottle-card__link:focus-visible .bottle-card__shine {
  opacity: 0.86;
}

.bottle-card__link:hover .bottle-card__light,
.bottle-card__link:focus-visible .bottle-card__light {
  filter: blur(22px);
  opacity: 0.5;
  transform: scale(1.08);
}

.bottle-card__link:hover .bottle-card__hover-card,
.bottle-card__link:focus-visible .bottle-card__hover-card {
  opacity: 1;
  transform: translate(-50%, 0) scale(1);
}

.bottle-card__link:active .bottle-card__image-frame {
  transform:
    translateY(-0.05rem)
    rotate(0deg)
    scale(0.995);
  transition-duration: 90ms;
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
    opacity: 0.3;
    transform: scale(1);
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

  .bottle-card__shine {
    display: none;
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
