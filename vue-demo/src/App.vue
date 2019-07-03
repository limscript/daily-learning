<template>
  <div id="app">
    <van-nav-bar
      title="vant"
      left-text="返回"
      left-arrow
    />
    <router-view />
    <van-tabbar v-model="active">
      <van-tabbar-item icon="home-o">
        标签
      </van-tabbar-item>
      <van-tabbar-item
        icon="search"
        dot
      >
        标签
      </van-tabbar-item>
      <van-tabbar-item
        icon="friends-o"
        info="5"
      >
        标签
      </van-tabbar-item>
      <van-tabbar-item
        icon="setting-o"
        info="20"
        @click="goDemo"
      >
        标签
      </van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      active: 0
    }
  },
  methods: {
    goDemo() {
      this.$router.push('/about')
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  :focus {
    outline: none;
  }
}
</style>
