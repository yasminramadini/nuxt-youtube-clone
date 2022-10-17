<template>
  <div class="bg-gray-800 h-full overflow-x-hidden">
    <navbar />
    <div class="wrapper">
      <sidebar />
      <nuxt />
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  display: grid;
  grid-template-columns: 23% auto;
}

@media screen and (max-width: 768px) {
  .wrapper {
    grid-template-columns: 100vw;
  }
}
</style>
