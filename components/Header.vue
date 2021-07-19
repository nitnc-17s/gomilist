<template lang="pug">
  div
    v-app-bar(dark app elevate-on-scroll)
      v-app-bar-nav-icon(@click="drawer = !drawer")
      v-toolbar-title(@click="top()" class="header-title") Gomi List
    v-navigation-drawer(v-model="drawer" app)
      v-list(nav dense)
        v-list-item-group
          v-list-item
            v-list-item-title(@click="top()") topへ戻る
          v-list-item
            v-list-item-title(@click="moveLink('https://www.city.yamatokoriyama.lg.jp/soshiki/cleancenter/gomi_recycle/26/1383.html')") 手引き
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({})
export default class Index extends Vue {
  /** data() */
  drawer = false

  /** methods() */
  top(){
    this.drawer = false
    this.$router.push('/')
  }

  moveLink(url:string){
    this.drawer = false
    window.open(url,'_blank')
  }

}
</script>

<style lang="scss" scoped>
.header-title{
  cursor: pointer;
}
</style>
