<template>
  <div class="vue-sk-lazy-image-box">
    <img class="vue-sk-lazy-image" ref="lazyImage" :src="isShowSrc" v-bind="$attrs">
  </div>
</template>

<script>
export default {
  props: {
    lazy: {
      type: Boolean,
      default: () => false
    }
  },
  data() {
    return {
      isShowSrc: ''
    }
  },
  mounted() {
    if (!this.lazy) {
      this.isShowSrc = this.$attrs.src
    }
    const io = new IntersectionObserver((entries) => {
      if (entries[0].intersectionRatio <= 0) return
      this.isShowSrc = this.$attrs.src
      io.unobserve(this.$refs.lazyImage)
    })
    io.observe(this.$refs.lazyImage)
  }
}
</script>

<style scoped>
.vue-sk-lazy-image-box {
  display: inline-block;
  width: 100%;
  height: 100%;
}
.vue-sk-lazy-image-box > .vue-sk-lazy-image {
  width: 100%;
  height: 100%;
}
</style>