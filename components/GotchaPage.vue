<template>
  <div>
    <div class="grid-centered grid-mainpage">
      <sky-cloud class="col-span-3 row-span-1 w-full self-start" />
      <aside class="col-span-1 row-span-2 h-full justify-self-start z-10 relative">
        <tree-left class="tree-left h-full" />
      </aside>
      <aside class="col-start-3 col-span-1 row-span-2 h-full justify-self-end z-10 relative">
        <tree-right class="tree-right h-full" />
      </aside>
      <aside class="row-start-3 row-span-1 col-start-2 col-span-1 z-20">
        <grass />
      </aside>
    </div>
    <main class="fixed top-0 left-0 w-screen h-screen z-0">
      <train :time="time" :delta-cabin-num="deltaCabinNum" :show-seat="showSeat" />
    </main>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  props: {
    time: {
      type: Number,
      default: 3000
    },
    deltaCabinNum: {
      type: Number,
      default: 90
    },
    showSeat: {
      type: Boolean,
      default: true
    }
  }
})
</script>

<style lang="postcss">
.grid-mainpage {
  display: grid;
  grid-template-rows: 20vh 60vh 20vh;
  grid-template-columns: 15vw 70vw 15vw;
  @apply w-screen h-screen;
}

.grid-centered {
  @apply grid justify-items-center items-center;
}
</style>
