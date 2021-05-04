<template>
  <div class="relative" style="height: auto; max-width: 50vw;">
    <img src="@/assets/train.png" alt="Cabin" style="height: auto; max-width: 50vw;">
    <div class="lang-tag">
      {{ languageToStringMapping[lang] }}
    </div>
    <div class="seat-tag">
      <div>{{ digitsOfRow[0] }}</div>
      <div>{{ digitsOfRow[1] }}</div>
      <div />
      <div>{{ colLetter }}</div>
      <div />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

/**
 * Validate integers in [a, b)
 */
function generateIntegerValidator (a: number, b: number) {
  return (val: number) => (Number.isInteger(val) && val >= a && val < b)
}

const languageToStringMapping = [
  'Basic', 'C/C++', 'Go', 'Java', 'JS', 'Lua',
  'Pascal', 'PHP', 'Python', 'R', 'Rust', 'SQL'
]

export default Vue.extend({
  props: {
    lang: {
      type: Number,
      default: 0,
      validator: generateIntegerValidator(0, 12)
    },
    row: {
      type: Number,
      default: 0,
      validator: generateIntegerValidator(0, 20)
    },
    col: {
      type: Number,
      default: 0,
      validator: generateIntegerValidator(0, 5)
    },
    showSeat: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      languageToStringMapping
    }
  },
  computed: {
    digitsOfRow () {
      return this.showSeat ? [String(Math.floor((this.row + 1) / 10)), String((this.row + 1) % 10)] : ['#', '#']
    },
    colLetter () {
      return this.showSeat ? (['A', 'B', 'C', 'D', 'E'])[this.col as number] : '#'
    }
  }
})
</script>

<style scoped lang="postcss">
@font-face {
  font-family: 'YouYuan';
  src: url("@/assets/YouYuan.ttf");
}

* {
  font-family: 'Comic Sans MS', 'YouYuan', monospace;
  font-size: 52px;
}

.lang-tag {
  position: absolute;
  top: 35%;
  left: 19%;
  width: 26%;
  display: grid;
  justify-items: center;
  color: #5b6752;
}

.seat-tag {
  position: absolute;
  top: 34%;
  left: 47%;
  width: 49%;
  height: 26%;
  color: #80bbd5;

  display: grid;
  grid-template-rows: 1fr;
  grid-template-columns: repeat(5, 1fr);
  gap: 3%;
  align-items: center;
  justify-items: center;
}

</style>
