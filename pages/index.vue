<template>
  <main class="pa3">
    <h1>Programmer's Quotes</h1>
    <nav class="pa2">
      <NuxtLink to="/about">About</NuxtLink>
      <h2>Authors</h2>
      <ul class="list pl0 center">
        <li
          v-for="authorLink in authorLinks"
          :key="authorLink.url"
          class="lh-copy pv3 ba bl-0 bt-0 br-0 b--dotted b--black-30"
        >
          <NuxtLink :to="authorLink.url">{{ authorLink.text }}</NuxtLink>
        </li>
      </ul>
    </nav>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  async asyncData({ $axios }) {
    const { data: authors = {} } = await $axios.get(
      'https://programming-quotes-api.herokuapp.com/Authors/'
    )

    const authorLinks = Object.keys(authors).map((author) => ({
      text: author,
      url: `/authors/${encodeURIComponent(author)}`,
    }))

    return { authorLinks }
  },
  head() {
    return {
      title: "Programmer's Quotes",
    }
  },
})
</script>
