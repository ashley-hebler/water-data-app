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
import { willPrefetch } from 'vue-apollo'
import list from '~/queries/list'
import gql from 'graphql-tag'

export default {
  data() {
    return {
      list: [],
      test: 'ashley',
      id: this.$route.params.state
    }
  },
  apollo: {
    list: {
      prefetch({ route }) {
        // => prefetch:true will not work as your query depends on route params
        return {
          id: route.params.state
        }
      },
      query: gql`
        query list($id: String!) {
          list(state: $id) {
            name
          }
        }
      `,
      variables() {
        return {
          id: this.id
        }
      }
    }
  },
  created() {
    console.log(this.test)
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
