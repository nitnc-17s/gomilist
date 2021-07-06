<template lang="pug">
  .wrapper
    Header.header
    nuxt
    Footer.footer
</template>

<style lang='scss'>
body {
  margin: 0;
  // overflow: hidden;
}
#app {
  min-height: 100%;
  position: relative;
}
.nuxt-box{
  height: 100%;
}
html, body, #__nuxt, #__layout, #__layout > div{
  min-height: 100vh;
}

.wrapper{
  position: relative;
  padding-bottom: $footer-h;
  box-sizing: border-box;
}

.header{
  height: $header-h;
}

.footer{
  height: $footer-h;
  width: 100%;
  position: absolute;
  bottom: 0;
}
</style>
