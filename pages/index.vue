<template>
  <div class="container">
    <search/>
  </div>
</template>

<script>
import Vue from 'vue'
import vueDebounce from 'vue-debounce'
 
Vue.use(vueDebounce);

export default {

  components: {
    Search: () => import('@/components/Search.vue')
  },

  mounted() {
  },

  methods: {
    
  }
}
</script>

