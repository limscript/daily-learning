<template>
  <div class="home">
    <images-viewer
      :titleable="false"
      :images="images"
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
const demoData = {
  啊实打实:
    '[{"id":"e7b19d72-42e5-b47f-eb82-00c7a395ebcb","user_id":"39e9fe5c-70cb-1376-6b16-65fa88d255f9","url":"https://img-test.myysq.com.cn/mobilecheckquality/upload/9ddbee37-7676-42d6-c86e-85ff04b7eb86.jpg"},{"id":"ca1bce04-400c-11cf-b901-22f20d4b31b0","size":267670,"duration":2000,"user_id":"39e9fe5c-70cb-1376-6b16-65fa88d255f9","url":"https://img-test.myysq.com.cn/mobilecheckquality/upload/57ca6acf-eeb3-4ea3-81aa-b9bbd11ebdfd.jpg","videoUrl":"https://img-test.myysq.com.cn/mobilecheckquality/upload/90ec9ac3-4184-fc68-2020-0cc1f7164084.mp4"},{"id":"c72b014d-8a09-1adc-973c-cb035a645379","user_id":"39e9fe5c-70cb-1376-6b16-65fa88d255f9","url":"https://img-test.myysq.com.cn/mobilecheckquality/upload/4e60a190-17f7-a280-efdf-0c502ae7913c.jpg"},{"id":"88fd3fec-1c83-047d-54c8-12f729a6fe5a","user_id":"39e9fe5c-70cb-1376-6b16-65fa88d255f9","url":"https://img-test.myysq.com.cn/mobilecheckquality/upload/aa55e7ed-55ec-1894-3586-b8af31f890b2.jpg"},{"id":"d7386540-c508-1a41-fb36-d1ec6b32fe33","user_id":"39e9fe5c-70cb-1376-6b16-65fa88d255f9","url":"https://img-test.myysq.com.cn/mobilecheckquality/upload/d2cecb2f-7159-de34-c62f-4a549598223d.jpg"}]'
}

export default {
  name: 'Home',
  components: {
    ImagesViewer
  },
  data() {
    return {
      images: []
    }
  },
  created() {
    let images = []
    Object.keys(demoData).forEach(item => {
      let arr = JSON.parse(demoData[item])
      arr.forEach(item2 => {
        item2.title = item
      })
      images = [...images, ...arr]
    })
    console.log(images)
    this.images = images
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
