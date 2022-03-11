<template>
  <main class="pa3">
    <h1>Author: {{ author.name }}</h1>
    <nav>
      <button @click="handleQuotesButtonClicked">Give me some quotes</button>
    </nav>
    <div class="pa3" v-html="rawHtml"></div>
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
        message: `Sorry, We don't have any data about the author "${params.author}".`,
      }
    }
    const wikiPage = author.wikiUrl.split('/').pop()

    const { data: wiki } = await $axios
      .get(
        `http://en.wikipedia.org/w/api.php?origin=*&action=parse&format=json&prop=text&section=0&page=${encodeURIComponent(
          wikiPage
        )}`
      )
      .catch(() => {
        throw {
          statusCode: 500,
          message: `Sorry, We couldn't get any data for "${params.author}".`,
        }
      })

    const rawHtml = wiki.parse
      ? wiki.parse.text['*'].replace(
          /\/wiki\//g,
          'https://en.wikipedia.org/wiki/'
        )
      : ''

    return { author, rawHtml }
  },
  head() {
    return {
      title: this.author.name,
    }
  },
  methods: {
    handleQuotesButtonClicked() {
      // This is a non-crawlable url to prove that 'quotes/*' pages are generated with an async function in nuxt.config.js
      this.$router.push({
        path: `/quotes/${encodeURIComponent(this.author.name)}`,
      })
    },
  },
}
</script>

