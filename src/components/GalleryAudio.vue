<template>
  <div class="row">
    <div class="col-sm-4 col-6 mb-4" v-for="(content, i) in contents" :key="i">
      <div class="card" style="width: 100%; border-radius: .75em;">
        <div
          class="gallery-vid"
          v-on:click="show(content.url, content.name, content.mime)"
        >
          <span class="material-icons icon-big">music_note</span>
        </div>
        <div class="card-body">
          <a :href="content.url" :download="content.name" class="content-center" target="blank" style="word-wrap: break-word;">
            <span class="material-icons">file_download</span> {{ content.name }}
          </a>
        </div>
      </div>
    </div>
  </div>

  <modal :active="active" v-on:submit="close" :title="title">
    <audio style="width:100%" ref="audioplayer" controls>
      <source :src="vid" :type="mime" />
      Your browser does not support the audio element
    </audio>
  </modal>
</template>

<script>
import ModalComp from "./ModalComp.vue"

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
      vid: "",
      title: "",
      mime: ""
    }
  },
  components: {
    'modal': ModalComp
  },
  methods: {
    close(val) {
      let audioku = this.$refs.audioplayer
      audioku.pause()

      this.active = val
    },
    show(url, title, mime) {
      this.vid = url
      this.title = title
      this.mime = mime

      let audioku = this.$refs.audioplayer
      audioku.load()

      this.active = true
    }
  }
}
</script>

<style>
.gallery-vid {
  width: 100%;
  height: 15em;
  border-radius: .75em .75em 0 0;
  background-image: linear-gradient(135deg, #ffe3b3, #53d2db);
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  cursor: zoom-in;
}
</style>