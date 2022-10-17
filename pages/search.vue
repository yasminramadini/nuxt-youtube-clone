<template>
  <main class="p-5">
    <p v-if="$fetchState.pending">Fetching data</p>
    <p v-else-if="$fetchState.error">Fetching error</p>
    <div class="mt-7 grid grid-cols-1 md:grid-cols-4 gap-4" v-else>
      <video-comp
        v-for="(video, index) in videos"
        :video="video"
        :key="index"
        class="mb-5"
      />
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      videos: [],
    };
  },
  async fetch() {
    await this.$axios
      .$get(
        `https://youtube-v31.p.rapidapi.com/search?q=${this.$route.query.keyword}&part=snippet,id&regionCode=ID&maxResults=50&order=date`,
        {
          headers: {
            "X-RapidAPI-Key":
              "502decae62mshb615cba2934462ap125953jsn933f8fcd95e7",
            "X-RapidAPI-Host": "youtube-v31.p.rapidapi.com",
          },
        }
      )
      .then((res) => {
        this.videos = res.items;
      });
  },
  watch: {
    "$route.query": "$fetch",
  },
};
</script>
