<template>
  <div class="home">
    <vue-viewer
      multiple
      :thumb="imageList"
      list-ul-class="image-list"
      :full="imageList"
    >
      <!--在列表中加入右上角删除按钮-->
      <template slot-scope="target">
        <span
          class="icon-remove"
          @click.stop="onRemove(target.index)"
          style=""
        >&times;</span>
      </template>
    </vue-viewer>
    <button
      type="button"
      @click="show"
    >Show</button>
  </div>
</template>

<script>
export default {
  name: 'Vievers',
  props: {
    // 底部预览小图
    navbar: {
      type: Boolean,
      default: true
    },
    // 工具栏
    toolbar: {
      type: Boolean,
      default: true
    },
    //
    tooltip: {
      type: Boolean,
      default: true
    },
    // 是否可移动
    movable: {
      type: Boolean,
      default: true
    },
    // 是否可缩放
    zoomable: {
      type: Boolean,
      default: true
    },
    // 是否可旋转
    rotatable: {
      type: Boolean,
      default: true
    },
    // 是否可镜像反转
    scalable: {
      type: Boolean,
      default: true
    },
    // 是否开启动画
    transition: {
      type: Boolean,
      default: true
    },
    // 是否可全屏
    fullscreen: {
      type: Boolean,
      default: true
    },
    // 是否开启键盘操控
    keyboard: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      options: {
        inline: false,
        title: true,
        button: false,
        navbar: this.navbar,
        toolbar: this.toolbar,
        tooltip: this.tooltip,
        movable: this.movable,
        zoomable: this.zoomable,
        rotatable: this.rotatable,
        scalable: this.scalable,
        transition: this.transition,
        fullscreen: this.fullscreen,
        keyboard: this.keyboard,
        url: 'data-source'
      },
      imageList: [
        'https://picsum.photos/346/216/?image=15',
        'https://picsum.photos/346/216/?image=16',
        'https://picsum.photos/346/216/?image=17',
        'https://picsum.photos/346/216/?image=18',
        'https://picsum.photos/346/216/?image=19',
        'https://picsum.photos/346/216/?image=20',
        'https://picsum.photos/346/216/?image=21',
        'https://picsum.photos/346/216/?image=12'
      ]
    }
  },
  methods: {
    inited(viewer) {
      this.$viewer = viewer
    },
    show() {
      this.$viewer.show()
    },
    onRemove(index) {
      alert(index)
    }
  }
}
</script>

<style>
.image-list {
  margin: 0;
  padding: 0;
}
.image-list li {
  display: inline-block;
  margin: 0 10px;
  list-style: none;
  position: relative;
}
.image-list li img {
  box-shadow: 0 0 5px #333;
}
.icon-remove {
  width: 20px;
  height: 20px;
  text-align: center;
  line-height: 20px;
  background: #f33;
  position: absolute;
  top: -10px;
  right: -10px;
  border-radius: 10px;
  cursor: pointer;
  color: #fff;
}
a {
  color: #42b983;
}
</style>
