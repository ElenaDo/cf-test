<template>
  <div>
    Loading...
  </div>
</template>

<style scoped>
@keyframes blink{
  0% {color: gray;}
  50% {color: black;}
  100% {color: gray;}
}
  div {
    animation: blink 1s infinite;
    min-height: 110px;
  }
</style>
