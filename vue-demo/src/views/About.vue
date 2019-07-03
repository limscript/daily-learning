<template>
  <div class="about">
    <div class="content">

      <div class="box"></div>
      <div class="box"></div>
      <div>{{deviceXDPI}}</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      deviceXDPI: 0
    }
  },
  created() {
    this.deviceXDPI = window.devicePixelRatio
  }
}
</script>
<style lang="scss" scoped>
.content {
  position: fixed;
  top: 100px;
  left: 0;
  right: 0;
}
.box {
  width: 100%;
  height: 10rem;
  background: blue;
}
</style>
