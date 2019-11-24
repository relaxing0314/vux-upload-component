<template>
  <li class="weui-uploader__file">
    <div class="weui-uploader__close"
      @click="remove(image, index)"
    ></div>
    <div class="weui-uploader__img"
      :style="style"
      @click="preview(image)"
    ></div>
  </li>
</template>

<script>
export default {
  props: {
    getUrl: {
      type: Object,
      default: () => {}
    },
    image: {
      type: Object,
      default: () => {}
    },
    index: {
      type: Number,
      default: 0
    }
  },
  computed: {
    style () {
      let imageUrl = `${this.image.url}`
      if(this.getUrl.fun && this.getUrl.key){
        imageUrl = this.getUrl.fun({
          key: this.image[this.getUrl.key]
        })
      }
      return {
        backgroundImage: `url(${imageUrl})`,
      }
    }
  },
  methods: {
    remove (image, index) {
      this.$emit('remove', { image, index })
    },
    preview (image) {
      this.$emit('preview', image)
    }
  }
}
</script>
<style lang="less" scoped>
  .weui-uploader__file{
    .weui-uploader__img{
      width: 100%;
      height: 100%;
      background: no-repeat center center;
      background-size: cover;
    }
    .weui-uploader__close{
      width: 18px;
      height: 18px;
      position: absolute;
      z-index: 2;
      top: 0;
      right: 0;
      font-size: 16px;
      background-color: rgba(0,0,0,.35);
      border-radius: 0;
      &:before{
        width: 2px;
        height: 12px;
        content: " ";
        position: absolute;
        top: 50%;
        left: 50%;
        transform: rotate(45deg) translate(-225%, -27%);
        background-color: rgba(255,255,255, 1);
      }
      &:after{
        width: 12px;
        height: 2px;
        content: " ";
        position: absolute;
        top: 50%;
        left: 50%;
        transform: rotate(45deg) translate(-37%, 195%);
        background-color: rgba(255,255,255,1);
      }
    }
  }
</style>
