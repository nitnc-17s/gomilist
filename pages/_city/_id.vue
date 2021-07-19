<template lang="pug">
  div
    v-list-item
      v-list-item-content
        v-list-item-subtitle 市
        v-list-item-title {{gomiData.city}}
    v-list-item
      v-list-item-content
        v-list-item-subtitle ゴミの名前
        v-list-item-title {{gomiData.name}}
    v-list-item
      v-list-item-content
        v-list-item-subtitle 分別方法
        v-list-item-title {{gomiData.separation}}
    v-list-item
      v-list-item-content
        v-list-item-subtitle カテゴリ
        v-list-item-title {{gomiData.category}}
    v-list-item(v-if="gomiData.notes.length")
      v-list-item-content
        v-list-item-subtitle 備考
        v-list-item-title(v-for="(note, ind) in gomiData.notes" :key="ind") {{note.note}}
    v-list-item(v-if="gomiData.garbage_days")
      v-list-item-content
        v-list-item-subtitle 分別日
        v-list-item-title(v-for="(day, ind) in gomiData.garbage_days" :key="ind") {{rWeekDay(day)}}
    //- v-list-item
    //-   v-list-item-content(v-if="gomiData.separation_notes.length")
    //-     v-list-item-subtitle 分別方法の詳細
    //-     v-list-item-title(v-for="(sNote, ind) in gomiData.separation_notes" :key="ind") {{sNote.note}}
    v-btn(class="mb-2 ml-4" :to="`/${this.$route.params.city}`") 戻る
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({
  async asyncData({ $axios, params }) {
    const gomiData = await $axios.$get(`/garbages/${params.id}`)
    console.log(gomiData)
    return {
      gomiData
    }
  }
})
export default class City extends Vue {
  /** data() */
  gomiData = {}

  /** methods() */
  rWeekDay(day:{dow:number, week:number}){
    let dow = ['日','月','火','水','木','金','土'][day.dow]
    let week = (day.week!==0)?`第${day.week}週` : '毎週'
    return `${week} ${dow}曜日`
  }
}
</script>

