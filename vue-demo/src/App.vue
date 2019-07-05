<template>
  <div id="app">
    <van-nav-bar
      v-if="page"
      title="vant"
      left-text="返回"
      left-arrow
    />
    <router-view />
    <van-tabbar
      v-if="page"
      v-model="active"
    >
      <van-tabbar-item icon="home-o">
        标签
      </van-tabbar-item>
      <van-tabbar-item
        icon="search"
        dot
        @click="pageTo('viewer')"
      >
        viewer
      </van-tabbar-item>
      <van-tabbar-item
        icon="friends-o"
        info="5"
        @click="pageTo('home')"
      >
        viewer
      </van-tabbar-item>
      <van-tabbar-item
        icon="setting-o"
        info="20"
        @click="pageTo('about')"
      >
        关于
      </van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      active: 0,
      page: true
    }
  },
  methods: {
    pageTo(router) {
      this.$router.push(`/${router}`)
      if (router !== 'about') {
        this.page = false
      }
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
