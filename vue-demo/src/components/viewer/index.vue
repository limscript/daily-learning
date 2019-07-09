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
            :data-original="img"
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
// 视频按钮
const videoButton = document.createElement('div')
videoButton.classList.add('viewer-video-button')

export default {
  name: 'ImagesViewer',
  components: {
    Viewer
  },
  props: {
    // 是否开启标题
    titleable: {
      type: Boolean,
      default: true
    },
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
          zoomIn: true, // 放大
          zoomOut: true, // 缩小
          prev: true, // 上一张
          next: true, // 下一张
          rotateLeft: true, // 左旋转
          rotateRight: true // 右旋转
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
      videoButton: videoButton,
      index: 0,
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
          this.viewChanged(item)
        }
      }
    }
  },
  methods: {
    // 初始化
    inited(viewer) {
      this.$viewer = viewer
    },
    // 打开图片预览
    show() {
      this.$viewer.show()
      this.$nextTick(() => {
        const viewerEl = this.$refs.viewer.$viewer.viewer
        const footerEl = this.$refs.viewer.$viewer.footer
        if (this.titleable) {
          viewerEl.appendChild(this.titleHtml)
        }
        if (this.remarkable && !this.navbar) {
          footerEl.appendChild(this.remarkHtml)
        }
      })
    },
    // 监听view事件
    viewChanged(item) {
      console.log(item)
      this.index = item.detail.index
      const viewerEl = this.$refs.viewer.$viewer.viewer
      // 视频
      if (this.images[this.index].videoUrl) {
        // 视频按钮
        viewerEl.appendChild(this.videoButton)
        this.videoButton.innerHTML = '<i class="van-icon van-icon-play-circle"></i>'
        this.videoButton.addEventListener('click', this.goVideoPage)
      } else {
        if (viewerEl.contains(this.videoButton)) {
          this.videoButton.removeEventListener('click', this.goVideoPage)
          viewerEl.removeChild(this.videoButton)
        }
      }
      // 标题
      if (this.titleable) {
        this.titleHtml.innerHTML = this.images[this.index].title
      }
      // 备注
      if (this.remarkable && !this.navbar) {
        this.remarkHtml.innerHTML = `<p>备注:</p><p>${this.images[this.index].remark}</p>`
      }
    },
    // 视频跳转
    goVideoPage() {
      const index = this.index
      console.log(this.images[index].videoUrl)
      let data = this.$router.resolve({
        name: 'Video',
        params: { url: this.images[index].videoUrl }
      })
      window.open(data.href, '_blank')
    }
  }
}
</script>
<style lang="scss">
.viewer-container {
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
  .viewer-canvas {
    padding-top: 20px;
  }
  .viewer-video-button {
    position: absolute;
    width: 100px;
    height: 100px;
    left: calc((100% - 100px) / 2);
    right: calc((100% - 100px) / 2);
    top: calc((100% - 100px) / 2);
    bottom: calc((100% - 100px) / 2);
    line-height: 100px;
    text-align: center;
    background: rgba(0, 0, 0, 0.5);
  }
}
</style>
