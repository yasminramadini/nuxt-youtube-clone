<template>
  <aside
    class="bg-gray-800 text-white p-5 border-r-0 md:border-r-2 border-gray-500 overflow-x-hidden sticky"
  >
    <ul class="flex flex-row md:flex-col md:gap-0 gap-8 overflow-x-auto">
      <li
        v-for="(category, index) in categories"
        :key="index"
        :class="category.name === activeMenu ? 'bg-red-500' : ''"
        class="hover:bg-gray-500 list-style-none py-3 pl-3 pr-5 md:pr-0 rounded"
        @click="setActiveMenu(category.name)"
      >
        <nuxt-link :to="category.url" class="flex items-center gap-5">
          <span class="material-symbols-outlined">{{ category.icon }}</span>
          {{ category.name }}
        </nuxt-link>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  methods: {
    setActiveMenu(menu) {
      this.activeMenu = menu;
    },
  },
  data() {
    return {
      activeMenu: "Home",
      categories: [
        {
          name: "Home",
          icon: "home",
          url: "/",
        },
        {
          name: "Gaming",
          icon: "stadia_controller",
          url: "/search?keyword=gaming",
        },
        {
          name: "Sports",
          icon: "sports_basketball",
          url: "/search?keyword=sports",
        },
        {
          name: "Coding",
          icon: "terminal",
          url: "/search?keyword=coding",
        },
        {
          name: "Cooking",
          icon: "cookie",
          url: "/search?keyword=cooking",
        },
        {
          name: "Movie",
          icon: "movie",
          url: "/search?keyword=movie",
        },
        {
          name: "Celebrity",
          icon: "auto_awesome",
          url: "/search?keyword=celebrity",
        },
        {
          name: "News",
          icon: "newspaper",
          url: "/search?keyword=news",
        },
        {
          name: "Podcasts",
          icon: "podcasts",
          url: "/search?keyword=podcast",
        },
        {
          name: "Religion",
          icon: "mosque",
          url: "/search?keyword=religion",
        },
      ],
    };
  },
  mounted() {
    const query =
      this.$route.query.keyword.charAt(0).toUpperCase() +
      this.$route.query.keyword.slice(1);
    this.activeMenu = query;
  },
};
</script>

<style scoped>
li {
  width: 100%;
  margin: 15px 0;
}

ul {
  scrollbar-width: 0;
}

ul::-webkit-scrollbar {
  display: none;
}

@media screen and (max-width: 768px) {
  aside {
    top: 2rem;
  }
}
</style>
