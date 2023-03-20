<template>
  <div class="vue-sk-lazy-image-box" :style="{ 'width': width || '100%', 'height': height || '100%' }">
    <img class="vue-sk-lazy-image" @error="handleLoadError" ref="lazyImage" :src="isShowSrc" v-bind="$attrs">
  </div>
</template>

<script>
export default {
  props: {
    lazy: {
      type: Boolean,
      default: () => false
    },
    width: {
      type: String,
      default: () => ''
    },
    height: {
      type: String,
      default: () => ''
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
  },
  methods: {
    handleLoadError(e) {
      console.log(e)
    }
  }
}
</script>

<style scoped>
.vue-sk-lazy-image-box {
  display: inline-block;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
.vue-sk-lazy-image-box > .vue-sk-lazy-image {
  width: 100%;
  height: 100%;
}
</style>