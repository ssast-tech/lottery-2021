<template>
  <div class="relative">
    <img src="@/assets/sky2.png" alt="Sky" :class="{'animate-bounce-sky': active}">
    <img src="@/assets/sky1.png" alt="Sky" :class="{'animate-bounce-sky-alt': active}">
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  props: {
    active: {
      type: Boolean,
      default: true
    }
  }
})
</script>

<style scoped lang="postcss">
  @keyframes bounce-sky {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-5%);
    }
  }
  .animate-bounce-sky {
    animation: bounce-sky 400ms ease-in-out infinite
  }
  .animate-bounce-sky-alt {
    animation: bounce-sky 400ms ease-in-out 200ms infinite
  }

  img {
    @apply absolute top-0 left-0;
  }
</style>
