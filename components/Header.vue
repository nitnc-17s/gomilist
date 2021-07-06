<template lang="pug">
  header.header
    Hamburger
    .title
      | Gomi List
</template>

<style lang="scss" scoped>
.header{
  position: relative;
  background-color: #89c7de;
  color: #fff;
  margin-bottom: $header-mar;
}

.title{
  @extend .center;
  font-size: 3vmax;
  @include sp{
    font-size: 2rem;
  }
}
</style>
