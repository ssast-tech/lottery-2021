<template>
  <img src="@/assets/tree-right.png" alt="Tree (Right Part)" class="tree-right">
</template>

<style scoped lang="postcss">
@keyframes tree-swing-right {
  0%, 50%, 100% {
    transform: scaleX(1);
  }
  5% {
    transform-origin: bottom right;
    transform: scaleX(1.2) rotate(3deg);
  }
  10%, 40% {
    transform: scaleX(1);
  }
  45% {
    transform-origin: bottom right;
    transform: scaleX(1.1);
  }
}
.tree-right {
  animation: tree-swing-right 5000ms ease-in 800ms infinite;
}
</style>
