<template>
  <main class="text-white p-5">
    <h3 v-if="$fetchState.pending">Fetching data</h3>
    <h3 v-else-if="$fetchState.error">Fetching error</h3>
    <section v-else>
      <img
        :src="video.snippet.thumbnails.medium.url"
        :alt="video.snippet.title"
        class="w-screen h-64 object-cover"
      />

      <section class="py-10 border-b-2 border-gray-600">
        <h3>{{ video.snippet.title }}</h3>
        <div
          class="grid grid-cols-1 md:grid-cols-2 justify-between overflow-x-auto text-sm md:text-base mt-5 gap-4"
        >
          <p class="text-gray-400">
            {{ formatNumber(video.statistics.viewCount) }}x ditonton - 20
            0ktober 2021
          </p>
          <div class="flex gap-5 items-center mt-4 md:mt-0">
            <p class="flex items-center gap-2">
              <span class="material-symbols-outlined">thumb_up</span>
              {{ formatNumber(video.statistics.likeCount) }}
            </p>
            <p class="flex items-center gap-2">
              <span class="material-symbols-outlined">thumb_down</span>
              Dislike
            </p>
            <p class="flex items-center gap-2">
              <span class="material-symbols-outlined">share</span>
              Share
            </p>
            <p class="flex items-center gap-2">
              <span class="material-symbols-outlined">bookmark</span>
              Save
            </p>
          </div>
        </div>
      </section>

      <section class="py-10 border-b-2 border-gray-600">
        <div class="flex gap-9 justify-between mb-8">
          <p class="font-bold mb-3">
            <nuxt-link :to="'/channel/' + video.snippet.channelId">{{
              video.snippet.channelTitle
            }}</nuxt-link>
          </p>
          <button
            class="bg-red-500 text-white py-2 px-3 border-0 outline-none rounded"
          >
            Subscribe
          </button>
        </div>
        <p class="text-gray-400">
          {{ video.snippet.description }}
        </p>
      </section>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      video: {},
    };
  },
  methods: {
    formatNumber(number) {
      return new Intl.NumberFormat("en-us").format(number);
    },
  },
  async fetch() {
    await this.$axios
      .$get(
        `https://youtube-v31.p.rapidapi.com/videos?part=contentDetails,snippet,statistics&id=${this.$route.params.id}`,
        {
          headers: {
            "X-RapidAPI-Key":
              "502decae62mshb615cba2934462ap125953jsn933f8fcd95e7",
            "X-RapidAPI-Host": "youtube-v31.p.rapidapi.com",
          },
        }
      )
      .then((res) => {
        this.video = res.items[0];
      });
  },
};
</script>
