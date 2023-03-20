<script>
import Vue from 'vue';
import VueSkLazyImage from '@/vue-sk-lazy-image.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueSkLazyImage
  }
});
</script>

<template>
  <div id="app">
    <div style="height: 1000px"></div>
    <vue-sk-lazy-image lazy x="12345" src="https://img.zcool.cn/community/0113b85b359893a80120b959eb69dd.jpg@1280w_1l_2o_100sh.jpg" />
  </div>
</template>
