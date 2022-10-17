<template>
  <main class="grid grid-cols-1 md:grid-cols-4 gap-4 p-5">
    <video-comp
      v-for="(video, index) in videos"
      :video="video"
      :key="index"
      class="mb-7"
    />
  </main>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      videos: [],
    };
  },
  async fetch() {
    await this.$axios
      .$get(
        "https://youtube-v31.p.rapidapi.com/search?relatedToVideoId=7ghhRHRP6t4&part=id,snippet&type=video&maxResults=50",
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
};
</script>
