<template>
  <div class="row">
    <div class="col-sm-4 col-6 mb-4" v-for="(content, i) in contents" :key="i">
      <div class="card" style="width: 100%; border-radius: .75em;">
        <a v-on:click="show(content.url, content.name)">
          <v-lazy-img
            :src="'https://hzm-thumbnailer.herokuapp.com/?u=' + content.url"
            class="gallery-img lazy"
            load="lazy"
            :alt="content.name"
          />
        </a>
        <div class="card-body">
          <a :href="content.url" :download="content.name" class="content-center" target="blank">
            <span class="material-icons">file_download</span> {{ content.name }}
          </a>
        </div>
      </div>
    </div>
  </div>

  <modal :active="active" v-on:submit="close" :title="title">
    <div class="text-center" v-if="img_load">
      <div class="spinner-border text-secondary" role="status"></div>
      <h5 class="text-secondary">{{ load_msg }}</h5>
    </div>

    <img :src="img" style="width: 100%" v-else/>
  </modal>
</template>

<script>
import ModalComp from "./ModalComp.vue"
import VLazyImage from "v-lazy-image";

export default {
  props: {
    contents: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      active: false,
      img: "",
      title: "",
      img_load: true,
      load_msg: 'Loading Full Size Image..'
    }
  },
  components: {
    'modal': ModalComp,
    'v-lazy-img': VLazyImage
  },
  methods: {
    close(val) {
      this.active = val
    },
    show(url, title) {
      this.img = url
      this.title = title
      this.img_load = true
      this.active = true

      let img = new Promise((resolve, reject) => {
        const img = new Image();
        img.src = url;
        img.onload = resolve;
        img.onerror = reject;
      });

      img.then(() => {
          this.img_load = false;
      }).catch((err) => {
          this.load_msg = "Failed to load image " + title
          console.log(err)
      })
    }
  }
}
</script>

<style>
.gallery-img {
  width: 100%;
  height: 15em;
  object-fit: cover;
  border-radius: .75em .75em 0 0;
  /* margin-bottom: .5em; */
  cursor: zoom-in;
}
</style>