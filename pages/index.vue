<template>
  <main class="flex flex-col items-center justify-center h-screen">
    <h1 class="mt-16 mb-16 font-sans text-4xl">
      2021软院学生节抽奖
    </h1>
    <div class="grid grid-cols-2 grid-rows-1">
      <nuxt-link class="focus:outline-none grid ring-4 ring-indigo-200 bg-indigo-700 hover:bg-indigo-600 text-white text-lg py-2 px-6 m-2 rounded-md" to="/normal/5000/75">
        <basket decorative class="mr-1" /><span class="col-start-2">普通抽奖</span>
      </nuxt-link>
      <nuxt-link class="focus:outline-none grid ring-4 ring-indigo-200 bg-indigo-700 hover:bg-indigo-600 text-white text-lg py-2 px-6 m-2 rounded-md" to="/final/10000/100">
        <shopping decorative class="mr-1" /><span class="col-start-2">大奖抽奖</span>
      </nuxt-link>
    </div>
  </main>
</template>

<script>
import Basket from 'vue-material-design-icons/Basket.vue'
import Shopping from 'vue-material-design-icons/Shopping.vue'
import Vue from 'vue'

export default Vue.extend({
  components: {
    Basket,
    Shopping
  }
})
</script>
