<template>
  <div class="wrip">
    <van-pull-refresh
      v-model="isLoading"
      @refresh="onRefresh"
    >
      <van-cell
        v-for="item in list"
        :key="item"
        :title="item"
      />
      <p>刷新次数: {{ count }}</p>
    </van-pull-refresh>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [],
      isLoading: false,
      count: 0
    }
  },
  methods: {
    onRefresh () {
      setTimeout(() => {
        this.$toast('刷新成功')
        this.list.push(this.count)
        this.isLoading = false
        this.count++
      }, 500)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.wrip {
  height: 100vh;
  overflow: hidden;
  margin: 0 0 -50px;
}
.van-pull-refresh {
  padding: 0 0 100px;
  overflow: auto;
  height: 100%;
  /deep/.van-pull-refresh__track {
    height: 100%;
    overflow: auto;
    padding: 0px 0px 100px;
  }
}
</style>
