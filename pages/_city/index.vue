<template lang="pug">
  v-card
    //- v-card-title ゴミリスト
    //- NuxtLink(:to="`/`" class="float-right") 戻る
    v-data-table(
      dense
      mobile-breakpoint="0"
      :headers="headers"
      :items="gomiList"
      :search="search"
      fixed-header
      disable-pagination
      hide-default-footer
      multi-sort
      loading = loading
      loading-text="Loading... Please wait"
    )
      template(v-slot:top)
        v-toolbar(flat)
          v-toolbar-title ゴミリスト
          v-spacer
          v-btn(:to="`/`") 戻る
        v-divider
        v-text-field(
          v-model="search"
          label="検索"
          class="mx-2"
        )
      template(v-slot:[`item.name`]="{ item }")
        NuxtLink(:to="toLink(String(item.id))") {{item.name}}
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'nuxt-property-decorator'

@Component({
  async asyncData({ $axios, params, error }) {
    let gomiList = await $axios.$get('/garbages', {params:{city:params.city}}).catch( e => error({ statusCode: 404, message: 'Post not found' }))
    gomiList = gomiList.garbages
    return {
      gomiList
    }
  }
})
export default class City extends Vue {
  /** data() */
  search=""
  loading = true
  headers = [
    {
      text: 'ゴミの名前',
      align: 'start',
      value: 'name',
      filter: this.filterGomiName,
    },
    { text: 'カテゴリ', value: 'category' },
    { text: '分別方法', value: 'separation' },
  ]
  gomiList: any[] = []

  @Watch('gomiList')
  onLoad() {
    this.loading = false
  }

  /** methods() */
  filterGomiName (value:string, search:string) {
    return value != null &&
      search != null &&
      value.indexOf(search) !== -1
  }

  toLink(id:string){
    return `/${this.$route.params.city}/${id}`
  }
}
</script>

<style lang="scss">
.v-data-table {
  td {
    background: #f0f8ff;
  }

  tr{
    &:nth-child(odd){
      td{
        background: #fff;
      }
    }

    &:hover{
      td{
        background: #eee;
      }
    }
  }
}
</style>
