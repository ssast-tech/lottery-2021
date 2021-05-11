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
        <cabin v-bind="x" :show-seat="showSeat" />
      </div>
    </ul>
    <div class="h-1/4 rail-container" />
  </div>
</template>

<script>
import Vue from 'vue'
import confetti from 'canvas-confetti'

function randBetween (a, b) {
  return Math.random() * (b - a) + a
}

const TRAIN_START_STATE = 10
const TRAIN_LENGTH = 120

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
  },
  data () {
    return {
      trainState: TRAIN_START_STATE + this.deltaCabinNum,
      cabins: [],
      transitionDisabled: false
    }
  },
  computed: {
    cssStyleLeft () {
      return `calc(-50vw * ${this.trainState})`
    },
    cssStyleTransition () {
      return this.transitionDisabled ? 'none' : `left ${this.time}ms ease-in-out`
    }
  },
  beforeMount () {
    this.shuffleCabins()
  },
  methods: {
    startTrain () {
      for (let i = -2; i <= 2; i++) {
        const temp = this.cabins[TRAIN_START_STATE + this.deltaCabinNum + i]
        this.cabins[TRAIN_START_STATE + this.deltaCabinNum + i] = this.cabins[TRAIN_START_STATE + i]
        this.cabins[TRAIN_START_STATE + i] = temp
      }

      this.transitionDisabled = true
      this.trainState = TRAIN_START_STATE
      this.shuffleCabins()

      setTimeout(function () {
        this.transitionDisabled = false
        this.trainState = TRAIN_START_STATE + this.deltaCabinNum
      }.bind(this), 0)
      setTimeout(confetti, this.time)
    },
    shuffleCabins () {
      const cabins = []
      for (let i = 0; i < TRAIN_LENGTH; i++) {
        cabins.push({
          lang: Math.floor(randBetween(0, 12-(1e-9))),
          row: Math.floor(randBetween(0, 20-(1e-9))),
          col: Math.floor(randBetween(0, 4-(1e-9))),
          id: Math.round(Math.random() * 1e8)
        })
      }
      if (this.cabins.length === 0) {
        this.cabins.splice(0, 0, ...cabins)
      } else {
        for (let i = TRAIN_START_STATE + 2; i < TRAIN_LENGTH; i++) {
          this.cabins[i] = cabins[i]
        }
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
