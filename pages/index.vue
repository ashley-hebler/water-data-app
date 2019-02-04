<template>
  <section>
    <section class="hero is-info is-bold">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">USA Rivers and Lakes</h1>
          <h2 class="subtitle">Choose a state</h2>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="container">
        <aside class="menu">
          <p class="menu-label">States</p>
          <ul v-for="(site) in list" :key="site.slug" class="menu-list">
            <li>
              <nuxt-link :to="{path: `/${site.slug}` }">{{ site.name }}</nuxt-link>
            </li>
          </ul>
        </aside>
      </div>
    </section>
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
