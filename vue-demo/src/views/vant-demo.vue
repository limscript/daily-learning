<template>
  <div class="wrip">
    <van-pull-refresh
      v-model="isLoading"
      @refresh="onRefresh"
    >
      <van-dropdown-menu>
        <van-dropdown-item
          v-model="value1"
          :options="options1"
        />
        <van-dropdown-item
          ref="item"
          title="筛选"
        >
          <van-switch-cell
            v-model="switch1"
            title="包邮"
          />
          <van-switch-cell
            v-model="switch2"
            title="团购"
          />
          <van-button
            block
            type="info"
            @click="onConfirm"
          >确认</van-button>
        </van-dropdown-item>
      </van-dropdown-menu>
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
import vanDropdownMenu from '../components/van-dropdown-menu'
import vanDropdownItem from '../components/van-dropdown-item'
export default {
  components: {
    vanDropdownMenu,
    vanDropdownItem
  },
  data() {
    return {
      list: [],
      isLoading: false,
      count: 0,
      value1: 0,
      value2: 'a',
      switch1: false,
      switch2: true,
      options1: [
        { text: '全部商品', value: 0 },
        { text: '新款商品', value: 1 },
        { text: '活动商品', value: 2 }
      ],
      options2: [
        { text: '默认排序', value: 'a' },
        { text: '好评排序', value: 'b' },
        { text: '销量排序', value: 'c' }
      ]
    }
  },
  methods: {
    onRefresh() {
      setTimeout(() => {
        this.$toast('刷新成功')
        this.list.push(this.count)
        this.isLoading = false
        this.count++
      }, 500)
    },
    onConfirm() {
      this.$refs.item.toggle()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.wrip {
  position: absolute;
  left: 0;
  right: 0;
  top: 46px;
  bottom: 50px;
  overflow: hidden;
  .van-pull-refresh {
    height: 100%;
    overflow: auto;
    .van-cell {
      text-align: center;
    }
    p {
      text-align: center;
    }
  }
}
</style>
