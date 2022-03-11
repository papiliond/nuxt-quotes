<template>
  <main>
    <header>
      <nav class="flex items-center cg2 pv2 ph2 pb1 bb">
        <button
          class="f6 link dim br1 ph3 pv2 mb2 dib white bg-purple"
          @click="$router.back()"
        >
          Back
        </button>
        <NuxtLink :to="'/'">Main page</NuxtLink>
      </nav>
    </header>
    <Nuxt />
  </main>
</template>

