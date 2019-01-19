<template>
  <section>
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">USA Rivers and Lakes</h1>
          <h2 class="subtitle">Choose a state</h2>
        </div>
      </div>
    </section>
    <div class="container">
      <div v-for="(site) in list" :key="site.slug" class="section">
        <nuxt-link :to="{path: `/${site.slug}` }">
          <h3 class="title">{{ site.name }}</h3>
        </nuxt-link>
      </div>
    </div>
  </section>
</template>

<script>
// import list from '~/queries/list'
// import Logo from '~/components/Logo.vue'
// import gql from 'graphql-tag'

export default {
  data() {
    return {
      list: [
        {
          name: 'Texas',
          slug: 'tx'
        },
        {
          name: 'Louisiana',
          slug: 'la'
        },
        {
          name: 'Colorado',
          slug: 'co'
        }
      ]
    }
  }
}
</script>

<style>
</style>
