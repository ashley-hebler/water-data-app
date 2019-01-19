<template>
  <section class="container">
    <nav class="breadcrumb" aria-label="breadcrumbs">
      <ul>
        <li><nuxt-link :to="{path: `/${state}` }">{{ state }}</nuxt-link></li>
        <li class="is-active">{{ id }}</li>
      </ul>
      
    </nav>
    <div v-for="(info, idx) in list" :key="idx">
      {{ info.name }}
      <div>
        <iframe
          :src="`https://maps.google.com/maps?q=${info.lat},${info.long}&hl=es;z=14&amp;output=embed`"
        />
      </div>
    </div>
    <div v-for="(measurement, idx) in item" :key="idx" class="tile">
      <h3 v-html="measurement.measureName"/>
      <div v-for="(val, idx2) in measurement.values" :key="measurement.measureName + idx2">
        <span v-if="idx2 < 3">
          <div>{{ val.value }} | {{ val.time }}</div>
        </span>
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
      id: this.$route.params.id,
      item: [],
      list: [],
      state: this.$route.params.state
    }
  },
  apollo: {
    item: {
      prefetch({ route }) {
        // => prefetch:true will not work as your query depends on route params
        return {
          id: route.params.id
        }
      },
      query: gql`
        query item($id: String!) {
          item(id: $id) {
            measureName
            values {
              time
              value
            }
          }
        }
      `,
      variables() {
        return {
          id: this.id
        }
      }
    },
    list: {
      prefetch({ route }) {
        // => prefetch:true will not work as your query depends on route params
        return {
          state: route.params.state,
          id: route.params.id
        }
      },
      query: gql`
        query list($state: String!, $id: String!) {
          list(state: $state, id: $id) {
            name
            lat
            long
          }
        }
      `,
      variables() {
        return {
          state: this.state,
          id: this.id
        }
      }
    }
  },
  created() {
    console.log(this.$route.params)
  }
}
</script>

<style>
</style>
