<template>
  <main class="p-5 text-white">
    <p v-if="$fetchState.pending">Fetching data</p>
    <p v-else-if="$fetchState.error">Fetching error</p>
    <div v-else>
      <img src="" alt="" />
      <section
        class="grid grid-cols-1 md:grid-cols-2 md:justify-between md:items-center my-7 gap-5"
      >
        <div class="flex gap-4 items-center">
          <img
            :src="channel.snippet.thumbnails.medium.url"
            :alt="channel.snippet.title"
            class="w-16 h-16 object-cover rounded-full"
          />
          <div>
            <h3>{{ channel.snippet.title }}</h3>
            <p class="text-gray-300">{{ formatNumber() }} subscribers</p>
          </div>
        </div>
        <button
          class="bg-red-500 text-white py-2 px-3 border-0 outline-none rounded inline-block md:ml-auto"
        >
          Subscribe
        </button>
      </section>

      <section class="py-4 bg-gray-900 p-5">
        <div class="grid grid-cols-1 md:grid-cols-2 justify-between gap-5">
          <div>
            <p class="mb-4">Description</p>
            <p class="text-gray-400 border-b-2 border-gray-600 pb-5">
              {{ channel.snippet.description }}
            </p>
          </div>
          <div>
            <p class="mb-4 border-b-2 border-gray-600">Statistics</p>
            <p class="mb-4 border-b-2 border-gray-600 pb-3">
              Joined at
              {{ new Date(channel.snippet.publishedAt).toUTCString() }}
            </p>
            <p class="mb-4 border-b-2 border-gray-600 pb-3">
              {{ formatNumber(channel.statistics.viewCount) }} x watched
            </p>
          </div>
        </div>
      </section>

      <section class="grid grid-cols-1 md:grid-cols-4 gap-5 mt-7">
        <video-comp
          v-for="(video, index) in videos"
          :video="video"
          :key="index"
        />
      </section>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      channel: {},
      videos: [],
    };
  },
  methods: {
    formatNumber() {
      return new Intl.NumberFormat("en-us").format(
        this.channel.statistics.subscriberCount
      );
    },
  },
  async fetch() {
    await this.$axios
      .$get(
        `https://youtube-v31.p.rapidapi.com/channels?part=snippet,statistics&id=${this.$route.params.id}`,
        {
          headers: {
            "X-RapidAPI-Key":
              "502decae62mshb615cba2934462ap125953jsn933f8fcd95e7",
            "X-RapidAPI-Host": "youtube-v31.p.rapidapi.com",
          },
        }
      )
      .then((res) => {
        this.channel = res.items[0];
      });
  },
};
</script>
