<script setup>
import InAppFooter from './components/inAppFooter.vue'
import InBarStage from './components/inBarStage.vue'
import InLinkMenu from './components/inLinkMenu.vue'
import InSiteHeader from './components/inSiteHeader.vue'
import InSkipLink from './components/inSkipLink.vue'
import { useReducedMotion } from './composables/useReducedMotion.js'
import { barLinks } from './data/barLinks.js'

const { prefersReducedMotion } = useReducedMotion()
</script>

<template>
  <div class="app-shell">
    <InSkipLink />

    <InSiteHeader />

    <main
      id="main-content"
      tabindex="-1"
    >
      <InBarStage
        :links="barLinks"
        :reduced-motion="prefersReducedMotion"
      />

      <InLinkMenu :links="barLinks" />
    </main>

    <InAppFooter :links="barLinks" />
  </div>
</template>
