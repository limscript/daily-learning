<template>
  <div class="viewer-wrap">
    <viewer
      :options="options"
      :images="images"
      @inited="inited"
      class="viewer"
      ref="viewer"
    >
      <template v-slot="scope">
        <div
          class="image-box"
          v-show="false"
        >
          <img
            v-for="(img,index) in scope.images"
            :src="img.url"
            :key="index"
          >
        </div>
      </template>
    </viewer>
  </div>
</template>

<script>
import 'viewerjs/dist/viewer.css'
import Viewer from 'v-viewer/src/component.vue'

// 标题
const titleHtml = document.createElement('div')
titleHtml.classList.add('view-title')
// 备注
const remarkHtml = document.createElement('div')
remarkHtml.classList.add('viewer-remark')

export default {
  name: 'ImagesViewer',
  components: {
    Viewer
  },
  props: {
    // 是否显示底部导航栏
    navbar: {
      type: Boolean,
      default: true
    },
    // 工具栏
    toolbar: {
      type: Object,
      default: () => {
        return {
          zoomIn: true,
          zoomOut: true,
          prev: true,
          next: true,
          rotateLeft: true,
          rotateRight: true
        }
      }
    },
    // 放大或缩小时显示的百分比的文字提示
    tooltip: {
      type: Boolean,
      default: true
    },
    // 是否开启备注,备注需关闭底部导航栏功能才能生效
    remarkable: {
      type: Boolean,
      default: false
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
    // 启用键盘支持
    keyboard: {
      type: Boolean,
      default: true
    },
    images: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data() {
    return {
      titleHtml: titleHtml,
      remarkHtml: remarkHtml,
      options: {
        inline: false,
        title: false,
        button: true,
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
        url: 'data-source',
        view: item => {
          const index = item.detail.index
          this.titleHtml.innerHTML = this.images[index].id
          if (this.remarkable && !this.navbar) {
            this.remarkHtml.innerHTML = `<p>备注:</p><p>${this.images[index].remark}</p>`
          }
        }
      }
    }
  },
  methods: {
    inited(viewer) {
      this.$viewer = viewer
    },
    show() {
      this.$viewer.show()
      this.$nextTick(() => {
        const viewerEl = this.$refs.viewer.$viewer.viewer
        const footerEl = this.$refs.viewer.$viewer.footer

        viewerEl.appendChild(this.titleHtml)
        if (this.remarkable && !this.navbar) {
          footerEl.appendChild(this.remarkHtml)
        }
      })
    }
  }
}
</script>
<style lang="scss">
.view-title {
  position: absolute;
  height: 48px;
  line-height: 48px;
  padding: 0 96px;
  font-size: 16px;
  color: #ffffff;
  font-weight: 500;
  text-align: center;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  top: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
.viewer-button {
  width: 48px;
  height: 48px;
  right: 0;
  top: 0;
  border-radius: 0;
  background-color: transparent;
  z-index: 10;
  &:hover {
    background-color: transparent;
  }
}
.viewer-toolbar > ul {
  margin: 0 auto 20px;
  > li {
    &:nth-child(3),
    &:nth-child(5) {
      margin: 0 0 0 20px;
    }
  }
}
.viewer-remark {
  height: 100px;
  box-sizing: border-box;
  padding: 10px 0 0;
  background-color: rgba(0, 0, 0, 0.5);
  > p {
    width: 720px;
    margin: 0 auto;
    line-height: 20px;
    text-align: left;
    font-size: 14px;
    color: #ffffff;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
  }
}
</style>
