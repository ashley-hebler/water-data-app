<template>
  <section class="container">
    <div>
      <div v-for="(site) in list" :key="site.id">
        <h3>{{ site.name }}</h3>
      </div>
    </div>
  </section>
</template>

<script>
import list from '~/queries/list'
import Logo from '~/components/Logo.vue'
import gql from 'graphql-tag'

export default {
  components: {
    Logo
  },
  data() {
    return {
      list: []
    }
  },
  // apollo: {
  //   list: {
  //     query: gql`
  //       query list {
  //         list {
  //           name
  //           id
  //         }
  //       }`
  //   },
  //   prefetch: true
  // }
  // apollo: {
  //   list: {
  //     prefetch: true,
  //     query: list,
  //     variables() {
  //       // Use vue reactive properties here
  //       return {
  //         state: 'tx'
  //       }
  //     }
  //   }
  // },
  apollo: {
    list: {
      prefetch: true,
      query: gql`
        query list($state: String!) {
          list(state: $state) {
            name
          }
        }
      `,
      variables() {
        return {
          state: 'la'
        }
      }
    }
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
