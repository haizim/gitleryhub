<template>
  <div class="container">
    <no-repo v-if="url == ''"></no-repo>

    <template v-if="loading">
      <no-repo message="Loading repository"></no-repo>
    </template>
    
    <template v-if="isError">
      <no-repo message="Are you sure it's real repository?"></no-repo>
    </template>

    <template v-if="!loading && url != '' && !isError">
      <div class="mb-3">
        <gallery-folder
          :contents="folders"
          v-on:submit="setPath"
          :path="path"
        ></gallery-folder>
      </div>
      <div class="d-flex mb-3">
        <a @click="setSection('images')" class="btn" :class="{ 'btn-primary': section == 'images' }">Images</a>
        <a @click="setSection('videos')" class="btn" :class="{ 'btn-primary': section == 'videos' }">Videos</a>
        <a @click="setSection('audios')" class="btn" :class="{ 'btn-primary': section == 'audios' }">Audios</a>
        <a @click="setSection('files')" class="btn" :class="{ 'btn-primary': section == 'files' }">Other Files</a>
      </div>

      <div v-show="section == 'images'">
        <gallery-image
          v-if="images.length > 0"
          :contents="images"
        ></gallery-image>

        <template v-if="images.length == 0">
          <no-repo message="I don't see any image here"></no-repo>
        </template>
      </div>

      <div v-show="section == 'videos'">
        <gallery-video
          v-if="videos.length > 0"
          :contents="videos"
        ></gallery-video>

        <template v-if="videos.length == 0">
          <no-repo message="I don't see any video here"></no-repo>
        </template>
      </div>

      <div v-show="section == 'audios'">
        <gallery-audio
          v-if="audios.length > 0"
          :contents="audios"
        ></gallery-audio>

        <template v-if="audios.length == 0">
          <no-repo message="I don't see any audio here"></no-repo>
        </template>
      </div>

      <div v-show="section == 'files'">
        <gallery-file
          v-if="files.length > 0"
          :contents="files"
        ></gallery-file>

        <template v-if="files.length == 0">
          <no-repo message="I don't see any file here"></no-repo>
        </template>
      </div>
    </template>
  </div>
</template>

<script>
import NoRepo from "./NoRepo.vue";
import GalleryImage from "./GalleryImage.vue";
import GalleryVideo from "./GalleryVideo.vue";
import GalleryAudio from "./GalleryAudio.vue";
import GalleryFolder from "./GalleryFolder.vue";
import GalleryFile from "./GalleryFile.vue";
// import VidVue from "./VidVue.vue"
import axios from 'axios';

export default {
  components: {
    "no-repo": NoRepo,
    "gallery-image": GalleryImage,
    "gallery-video": GalleryVideo,
    "gallery-audio": GalleryAudio,
    "gallery-folder": GalleryFolder,
    "gallery-file": GalleryFile
  },
  props: {
    url: {
      default: "",
    },
  },
  data() {
    return {
      files: [],
      folders: [],
      images: [],
      videos: [],
      audios: [],
      loading: false,
      section: 'images',
      path: '',
      isError: false
    }
  },
  methods: {
    async getData(url) {
      this.isError = false
      const backend = 'https://gitleryhub.haizim.one/ajax'
      // const backend = 'http://localhost:8'
      if (url != '') {
        try {
          this.loading = true
          let get = await axios.get(`${backend}?repo=${url}&path=${this.path}`)
          console.log(get)
          let data = get.data
          console.log(data.data)
          this.files = data.data.file
          this.folders = data.data.folder
          this.images = data.data.image
          this.videos = data.data.video
          this.audios = data.data.audio

          if (this.images.length > 0) {
            this.section = 'images'
          } else if (this.videos.length > 0) {
            this.section = 'videos'
          } else if (this.audios.length > 0) {
            this.section = 'audios'
          } else if (this.files.length > 0) {
            this.section = 'files'
          } else {
            this.section = 'images'
          }
        } catch (error) {
          this.isError = true
        } finally {
          this.loading = false
        }
      }
    },
    setSection(sect) {
      this.section = sect
    },
    setPath(val) {
      this.path = val
    }
  },
  watch: {
    url: async function(val) {
      console.log('url : ', val)
      this.path = ''
      await this.getData(val)
    },
    path: async function(val) {
      console.log('path : ', val)
      await this.getData(this.url)
    },
  }
};
</script>
