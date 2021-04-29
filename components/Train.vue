<template>
  <div class="w-screen h-screen overflow-hidden">
    <div class="h-1/4" />
    <ul
      class="cabin-container flex flex-row overflow-hidden h-1/2 top-1"
      :style="{
        transition: cssStyleTransition,
        left: cssStyleLeft,
        position: 'relative'
      }"
    >
      <div
        v-for="x in cabins"
        :key="x.id"
        class="flex flex-col-reverse cursor-pointer"
        @click="startTrain"
      >
        <cabin v-bind="x" />
      </div>
    </ul>
    <div class="h-1/4 rail-container" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

function randBetween (a: number, b: number) {
  return Math.random() * (b - a) + a
}

export default Vue.extend({
  data () {
    return {
      trainState: 100,
      cabins: [],
      transitionDisabled: false
    }
  },
  computed: {
    cssStyleLeft () {
      return `calc(-50vw * ${this.trainState})`
    },
    cssStyleTransition () {
      return this.transitionDisabled ? 'none' : 'left 3000ms ease-in-out'
    }
  },
  beforeMount () {
    this.shuffleCabins()
  },
  methods: {
    startTrain () {
      for (let i = 0; i < 20; i++) {
        const temp = this.cabins[i + 90]
        this.cabins[i + 90] = this.cabins[i]
        this.cabins[i] = temp
      }

      this.transitionDisabled = true
      this.trainState = 10
      setTimeout(function () {
        this.transitionDisabled = false
        this.trainState = 100
        this.shuffleCabins()
      }.bind(this), 0)
    },
    shuffleCabins () {
      const trainLength = 120
      this.cabins = []
      for (let i = 0; i < trainLength; i++) {
        this.cabins.push({
          lang: Math.floor(randBetween(0, 11)),
          row: Math.floor(randBetween(0, 19)),
          col: Math.floor(randBetween(0, 4)),
          id: Math.round(Math.random() * 1e8)
        })
      }
    }
  }
})
</script>

<style scoped lang="postcss">
* {
  box-sizing: border-box;
}
.rail-container {
  background: url("@/assets/rail.png") repeat-x;
  background-size: auto 100%;
}

.cabin-container {
  width: 10000vw;
  padding-left: 25%;
}
</style>
