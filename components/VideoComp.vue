<template>
  <div class="card">
    <img
      :src="video.snippet.thumbnails.medium.url"
      :alt="video.snippet.title"
      class="w-full"
    />
    <h3 class="text-white mt-2">
      <nuxt-link :to="'/video/' + video.id.videoId">{{
        video.snippet.title
      }}</nuxt-link>
    </h3>
    <p class="text-gray-400 mt-3">{{ video.snippet.channelTitle }}</p>
  </div>
</template>

<script>
export default {
  props: {
    video: Object,
  },
};
</script>
