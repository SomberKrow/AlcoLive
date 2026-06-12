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
  const values = ['-0.7deg', '0.48deg', '-0.24deg', '0.62deg', '-0.42deg']

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
  const rotateY = ((x - 50) / 50) * 3.4
  const rotateX = ((50 - y) / 50) * 2.2

  target.style.setProperty('--rx', `${rotateX.toFixed(2)}deg`)
  target.style.setProperty('--ry', `${rotateY.toFixed(2)}deg`)
}

function resetPointer(event) {
  const target = event.currentTarget

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
  --bottle-width: clamp(7.1rem, 8.15vw, 9.45rem);
  --bottle-height: clamp(13.25rem, 17vw, 18.8rem);
  --rx: 0deg;
  --ry: 0deg;

  position: relative;
  flex: 0 0 auto;
  width: calc(var(--bottle-width) + 0.35rem);
  min-height: calc(var(--bottle-height) + 1.05rem);
  perspective: 900px;
  scroll-snap-align: center;
}

.bottle-card__link {
  position: relative;
  display: grid;
  min-height: calc(var(--bottle-height) + 1.05rem);
  place-items: end center;
  isolation: isolate;
}

.bottle-card__link:focus-visible {
  outline-offset: 0.42rem;
}

.bottle-card__light {
  position: absolute;
  right: 0.25rem;
  bottom: 0.02rem;
  left: 0.25rem;
  z-index: -1;
  height: 44%;
  background:
    radial-gradient(
      ellipse at 50% 78%,
      color-mix(in srgb, var(--accent), transparent 56%),
      transparent 72%
    ),
    radial-gradient(ellipse at 50% 100%, rgba(255, 196, 112, 0.16), transparent 58%);
  filter: blur(18px);
  opacity: 0.24;
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
    translateY(0.82rem)
    rotate(var(--tilt))
    rotateX(0deg)
    rotateY(0deg)
    scale(0.97);
  transform-origin: 50% 96%;
  transform-style: preserve-3d;
  filter:
    saturate(0.98)
    contrast(1.02)
    brightness(0.98)
    drop-shadow(0 1.05rem 0.72rem rgba(0, 0, 0, 0.56))
    drop-shadow(0 0 0.42rem color-mix(in srgb, var(--accent), transparent 90%));
  animation: bottleSettle 620ms var(--ease-bounce) var(--stagger) forwards;
  transition:
    filter var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-bounce);
  will-change: transform, filter;
}

.bottle-card__image-frame::before {
  position: absolute;
  right: 16%;
  bottom: 0.08rem;
  left: 16%;
  z-index: 1;
  height: 0.78rem;
  content: '';
  background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.72), transparent 74%);
  filter: blur(5px);
  opacity: 0.9;
  transform: translateZ(-1px) scaleX(0.94);
  transition:
    opacity var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-standard);
}

.bottle-card__image-frame::after {
  position: absolute;
  right: 11%;
  bottom: -0.28rem;
  left: 11%;
  z-index: 0;
  height: 1.55rem;
  content: '';
  background:
    radial-gradient(
      ellipse at center,
      color-mix(in srgb, var(--accent), transparent 76%),
      transparent 66%
    ),
    radial-gradient(ellipse at center, rgba(255, 176, 86, 0.12), transparent 72%);
  filter: blur(8px);
  opacity: 0.48;
  transform: scaleX(0.9);
  transition:
    opacity var(--duration-medium) var(--ease-standard),
    transform var(--duration-medium) var(--ease-standard);
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
  transform: translateZ(18px);
}

.bottle-card__hover-card {
  position: absolute;
  bottom: 0.35rem;
  left: 50%;
  z-index: 20;
  display: grid;
  width: min(11.75rem, 88vw);
  gap: 0.16rem;
  padding: 0.62rem 0.72rem;
  pointer-events: none;
  background:
    radial-gradient(circle at 50% 0%, color-mix(in srgb, var(--accent), transparent 84%), transparent 58%),
    rgba(9, 7, 6, 0.88);
  border: 1px solid color-mix(in srgb, var(--accent), transparent 48%);
  border-radius: var(--radius-md);
  box-shadow:
    0 16px 34px rgba(0, 0, 0, 0.46),
    0 0 18px color-mix(in srgb, var(--accent), transparent 80%);
  opacity: 0;
  transform: translate(-50%, 0.42rem) scale(0.96);
  transition:
    opacity var(--duration-fast) var(--ease-standard),
    transform var(--duration-fast) var(--ease-standard);
  backdrop-filter: blur(10px);
}

.bottle-card__hover-card small {
  color: color-mix(in srgb, var(--accent), var(--color-neon-gold) 28%);
  font-size: 0.58rem;
  font-weight: 950;
  letter-spacing: 0.16em;
  line-height: 1;
  text-transform: uppercase;
}

.bottle-card__hover-card strong {
  color: var(--color-cream);
  font-family: var(--font-display);
  font-size: 1.06rem;
  letter-spacing: -0.04em;
  line-height: 1;
}

.bottle-card__hover-card span {
  color: rgba(246, 230, 200, 0.74);
  font-size: 0.72rem;
  line-height: 1.32;
}

.bottle-card__link:hover .bottle-card__image-frame,
.bottle-card__link:focus-visible .bottle-card__image-frame {
  filter:
    saturate(1.08)
    contrast(1.05)
    brightness(1.08)
    drop-shadow(0 1.3rem 0.95rem rgba(0, 0, 0, 0.62))
    drop-shadow(0 0 0.82rem color-mix(in srgb, var(--accent), transparent 76%));
  transform:
    translateY(-0.18rem)
    rotate(0deg)
    rotateX(var(--rx))
    rotateY(var(--ry))
    scale(1.022);
}

.bottle-card__link:hover .bottle-card__image-frame::before,
.bottle-card__link:focus-visible .bottle-card__image-frame::before {
  opacity: 0.72;
  transform: translateZ(-1px) scaleX(1.08);
}

.bottle-card__link:hover .bottle-card__image-frame::after,
.bottle-card__link:focus-visible .bottle-card__image-frame::after {
  opacity: 0.68;
  transform: scaleX(1.14);
}

.bottle-card__link:hover .bottle-card__light,
.bottle-card__link:focus-visible .bottle-card__light {
  filter: blur(21px);
  opacity: 0.46;
  transform: scale(1.08);
}

.bottle-card__link:hover .bottle-card__hover-card,
.bottle-card__link:focus-visible .bottle-card__hover-card {
  opacity: 1;
  transform: translate(-50%, 0) scale(1);
}

.bottle-card__link:active .bottle-card__image-frame {
  transform:
    translateY(-0.02rem)
    rotate(0deg)
    scale(0.996);
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
    transform: translateY(0.82rem) rotate(var(--tilt)) scale(0.97);
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
