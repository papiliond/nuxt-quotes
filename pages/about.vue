<template>
  <main>
    <h1>About page</h1>
    <button
      class="f6 link dim br1 ph3 pv2 mb2 dib white bg-purple"
      @click="$router.back()"
    >
      Back
    </button>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
})
</script>
