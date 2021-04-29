<template>
  <img src="@/assets/tree-left.png" alt="Tree (Left Part)" class="tree-left">
</template>

<style scoped lang="postcss">

@keyframes tree-swing-left {
  0%, 50%, 100% {
    transform: scaleX(1);
  }
  5% {
    transform-origin: bottom left;
    transform: scaleX(1.2);
  }
  10%, 40% {
    transform: scaleX(1);
  }
  45% {
    transform-origin: bottom left;
    transform: scaleX(1.1) rotate(-3deg);
  }
}

.tree-left {
  animation: tree-swing-left 5000ms ease-in infinite;
}
</style>
