<template>
  <div class="home">
    <images-viewer
      :images="images"
      :navbar="false"
      :remarkable="true"
      ref="imagesViewer"
    />
    <button
      type="button"
      @click="show"
    >Show</button>
  </div>
</template>

<script>
import ImagesViewer from '@/components/viewer'

export default {
  name: 'Home',
  components: {
    ImagesViewer
  },
  data() {
    return {
      images: [
        {
          id: 1,
          url: 'https://picsum.photos/346/216/?image=15',
          remark:
            '暗示收到公司的个十多个第zcx按时发放十大歌手广东省高十多个十多个十多个十多个申达股份十多个三个十多个十多个十多个十多个收到公司的个十多个十多个' +
            '十多个十大歌手感受到十多个十多个第三个第三个十多个十多个收到公司的广东省十多个的归属感十多个的归属感十多个十多个第三个颂德歌功法法师'
        },
        { id: 2, url: 'https://picsum.photos/346/216/?image=16', remark: '暗示法法师' },
        {
          id: 3,
          url: 'https://picsum.photos/346/216/?image=17',
          remark: '暗示法性大发沙发沙发斯蒂芬法师'
        },
        { id: 4, url: 'https://picsum.photos/346/216/?image=18', remark: '暗示法法十多个施工是师' },
        { id: 5, url: 'https://picsum.photos/346/216/?image=19', remark: '暗示法法师' },
        {
          id: 6,
          url: 'https://picsum.photos/346/216/?image=20',
          remark: '暗示法法收到公司的公司的第三个十多个十多个十多个十多个师'
        },
        { id: 7, url: 'https://picsum.photos/346/216/?image=21', remark: '暗示法法师' },
        { id: 8, url: 'https://picsum.photos/346/216/?image=12', remark: '暗示法法师' }
      ]
    }
  },
  methods: {
    // 打开
    show() {
      this.$refs.imagesViewer.show()
    }
  }
}
</script>
<style lang="scss">
</style>
