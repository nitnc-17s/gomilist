<template lang="pug">
  .wrapper
    .text
      div エラーが発生しました
      nuxt-link(to="/") 戻る
</template>

<style lang="scss" scoped>
.wrapper{
  height: calc(100vh - 220px);
}

.text{
  @extend .center;
  text-align: center;
}
</style>
