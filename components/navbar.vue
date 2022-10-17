<template>
  <nav
    class="bg-gray-800 py-3 px-5 md:p-5 flex justify-between items-center gap-10 sticky top-0 z-50"
  >
    <img
      src="~/assets/img/youtube.png"
      alt="logo youtube"
      width="70"
      class="grow-0"
    />
    <form class="flex items-center grow" action="/search" method="GET">
      <input
        type="text"
        class="bg-gray-900 px-3 py-2 text-white block w-full"
        placeholder="Search..."
        name="keyword"
        v-model="keyword"
      />
      <button>
        <span class="material-symbols-outlined bg-gray-500 text-white p-2"
          >search</span
        >
      </button>
    </form>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      keyword: "",
    };
  },
};
</script>

<style scoped>
input,
button {
  outline: none;
  border: none;
}
</style>
