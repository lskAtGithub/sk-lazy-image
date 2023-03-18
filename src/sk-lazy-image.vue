<template>
  <div class="sk-lazy-image-box">
    <img ref="lazyImage" :src="isShowSrc" v-bind="$attrs">
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
      console.log(entries[0].intersectionRatio)
      if (entries[0].intersectionRatio <= 0) return
      this.isShowSrc = this.$attrs.src
      io.unobserve(this.$refs.lazyImage)
    })
    io.observe(this.$refs.lazyImage)
  }
}
</script>

<style scoped>
.sk-lazy-image-box {
  display: inline-block;
}
</style>