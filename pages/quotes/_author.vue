<template>
  <main class="pa3">
    <h1>Quotes from {{ author.name }}</h1>
    <mav class="flex mb3">
      <NuxtLink :to="`/authors/${encodeURIComponent(author.name)}`"
        >Author's page</NuxtLink
      >
    </mav>
    <div class="flex flex-column">
      <q v-for="quote in author.quotes" :key="quote.id" class="pa2">
        {{ quote.en }}</q
      >
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    const { data: author } = await $axios.get(
      'https://programming-quotes-api.herokuapp.com/Authors/' +
        encodeURIComponent(params.author)
    )
    if (!author.quotes || !author.quotes.length) {
      throw {
        statusCode: 404,
        message: `Sorry, We don't have any quotes from "${params.author}".`,
      }
    }

    return { author }
  },
  head() {
    return {
      title: 'Quotes from ' + this.author.name,
    }
  },
}
</script>

