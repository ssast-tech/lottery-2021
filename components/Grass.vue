<template>
  <img src="@/assets/grass.png" alt="Grass" class="grass">
</template>

<style scoped lang="postcss">
@keyframes grass-swing {
  0%, 10%, 40%, 50%, 100% {
    transform: skew(0deg, 0deg);
  }
  5% {
    transform: skew(5deg, 0deg);
  }
  45% {
    transform: skew(-5deg, 0deg);
  }
}

.grass {
  animation: grass-swing 2000ms infinite;
}
</style>
