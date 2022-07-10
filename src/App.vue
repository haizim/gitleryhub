<template>
  <repo-address v-model="url" v-on:submit="gallery"></repo-address>

  <div class="container py-3">
    <show-gallery :url="url"></show-gallery>
  </div>

  <div class="bg-light text-center text-secondary py-2 mt-2">
    si <a href="https://haizim.one/" target="blank">haizim</a> lagi gabut trus
    bikin ini
  </div>
</template>

<script>
import RepoAddress from "./components/RepoAddress.vue";
import ShowGallery from "./components/ShowGallery.vue";

export default {
  data() {
    return {
      url: "",
    };
  },

  components: {
    RepoAddress,
    ShowGallery,
  },

  methods: {
    gallery(value) {
      this.url = value;
      console.log(value);
    },
  },
};
</script>
