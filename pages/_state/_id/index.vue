<template>
  <section class="container">
    <div v-for="(info, idx) in list" :key="idx">
      <nav class="navbar" role="navigation" aria-label="main navigation">
        <nav class="breadcrumb is-medium" aria-label="breadcrumbs">
          <ul>
            <li>
              <nuxt-link :to="{path: `/` }">All</nuxt-link>
            </li>
            <li>
              <nuxt-link :to="{path: `/${state}` }">{{ state | stateName }}</nuxt-link>
            </li>
            <li class="is-active"><a href="#" aria-current="page">{{ info.name }}</a></li>
          </ul>
        </nav>
      </nav>

      <section class="hero is-info is-bold">
        <div class="hero-body">
          <div class="container">
            <h1 class="title">{{ info.name }}</h1>
            <h2 class="subtitle">{{ info.city }}, {{ state | stateName }}</h2>
          </div>
        </div>
      </section>
      <div>
        <iframe
          :src="`https://maps.google.com/maps?q=${info.lat},${info.long}&hl=es;z=14&amp;output=embed`"
          width="100%"
        />
      </div>
    </div>
    <section class="columns is-multiline">
      <div v-for="(measurement, idx) in item" :key="idx" class="column is-one-third">
        <div class="card">
          <header class="card-header">
            <h3 class="card-header-title" v-html="measurement.measureName"/>
            <span class="card-header-icon">
              <h4 class="tag is-primary">Avg: {{ measurement.measureAvg }}</h4>
            </span>
          </header>
          <div class="card-content">
            <div class="content">
              <div v-for="(val, idx2) in measurement.values" :key="measurement.measureName + idx2">
                <span v-if="idx2 < 3">
                  <div>{{ val.value }} | {{ prettyDate(val.time) }}</div>
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
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
          id: route.params.id,
          state: route.params.state
        }
      },
      query: gql`
        query item($id: String!, $state: String!) {
          item(id: $id, state: $state) {
            measureName
            measureAvg
            values {
              time
              value
            }
          }
        }
      `,
      variables() {
        return {
          id: this.id,
          state: this.state
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
            city
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
  },
  methods: {
    prettyDate(date) {
      const temp = date
        .split('T')[0]
        .split('-')
        .reverse()
      let newFormat
      temp[0] = temp.splice(1, 1, temp[0])[0]
      newFormat = temp.join('/')
      if (newFormat.charAt(0) === '0') {
        newFormat = newFormat.slice(1)
      }
      return newFormat
    }
  }
}
</script>

<style>
</style>
