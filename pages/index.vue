<template>
  <div>
    <h1>Nuxt demo</h1>
    <nav>
      <NuxtLink to="/about">About</NuxtLink>
      <NuxtLink to="/quotes/Edsger%20W.%20Dijkstra"
        >Quotes from Dijkstra</NuxtLink
      >
    </nav>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
})
</script>
