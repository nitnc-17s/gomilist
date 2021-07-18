<template lang="pug">
  v-list
    v-list-item-title 奈良県
    v-divider
    v-list-item(
      v-for="city in cityList"
      :key="city.id"
      @click="$router.push(String(city.id))"
    ) {{city.name}}
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import city from '@/assets/city/city.json'

@Component({})
export default class Index extends Vue {
  /** data() */
  cityList: any[]= []

  /** beforeMount() */
  beforeMount() {
    this.cityList.push(...city)
  }
}
</script>

