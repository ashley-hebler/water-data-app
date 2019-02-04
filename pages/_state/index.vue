<template>
  <section class="container">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <nav class="breadcrumb is-medium" aria-label="breadcrumbs">
        <ul>
          <li>
            <nuxt-link :to="{path: `/` }">All</nuxt-link>
          </li>
          <li class="is-active"><a href="#" aria-current="page">{{ state | stateName }}</a></li>
        </ul>
      </nav>
    </nav>
    <section class="hero is-info is-bold">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">{{ $route.params.state | stateName }}</h1>
          <h2 class="subtitle">Rivers and Lakes</h2>
        </div>
      </div>
    </section>
    <div class="panel">

      <div v-for="(site, index) in list" :key="site.id + index" class="panel-block">
        <nuxt-link :to="{path: `/${$route.params.state}/${site.id}` }">{{ site.name }}</nuxt-link>
      </div>
    </div>
    <div class="panel-block">
      <button
        v-if="$apollo.queries.list.loading"
        class="button is-link is-outlined is-fullwidth"
      >Loading...</button>
      <button
        v-else-if="showMoreEnabled"
        class="button is-link is-outlined is-fullwidth"
        @click="showMore"
      >More
        <Observer @intersect="showMore"/>
      </button>
    </div>
  </section>
</template>

<script>
import Observer from '~/components/Observer.vue'
import { willPrefetch } from 'vue-apollo'
import list from '~/queries/list'
import gql from 'graphql-tag'

const SITES_PER_PAGE = 100

export default {
  components: {
    Observer
  },
  data() {
    return {
      list: [],
      listMore: [],
      test: 'ashley',
      state: this.$route.params.state,
      start: 1,
      end: SITES_PER_PAGE,
      skipQuery: true,
      loading: false,
      showMoreEnabled: true
    }
  },

  apollo: {
    list: {
      prefetch({ route }) {
        // => prefetch:true will not work as your query depends on route params
        return {
          state: route.params.state,
          start: 1,
          end: SITES_PER_PAGE
        }
      },
      query: gql`
        query list($state: String!, $start: Int!, $end: Int!) {
          list(state: $state, start: $start, end: $end) {
            name
            id
          }
        }
      `,
      variables() {
        return {
          state: this.state,
          start: 1,
          end: SITES_PER_PAGE
        }
      }
    }
  },
  mounted() {},
  methods: {
    updateCount(start, end) {
      return new Promise(resolve => {
        this.loading = true
        this.start = start
        this.end = end
        let data = {
          start: start,
          end: end
        }
        resolve(data)
      })
    },
    blah() {
      console.log('hi!')
    },
    showMore() {
      let start = this.list.length + 1
      let end = start + SITES_PER_PAGE
      let state = this.state
      let vm = this
      console.log(start)
      console.log(end)
      this.updateCount(start, end).then(data => {
        // Fetch more data and transform the original result
        vm.$apollo.queries.list.fetchMore({
          // New variables
          variables: {
            state: state,
            start: data.start,
            end: data.end
          },
          // Transform the previous result with new data
          updateQuery: (previousResult, { fetchMoreResult }) => {
            const newTags = fetchMoreResult.list
            let oldList = vm.list
            vm.loading = false
            const hasMore = fetchMoreResult.list.length > 0
            console.log(hasMore)
            vm.showMoreEnabled = hasMore
            return Object.assign({}, previousResult, {
              list: oldList.concat(newTags),
              hasMore
            })
          }
        })
      })
    }
  }
}
</script>

<style>
</style>
