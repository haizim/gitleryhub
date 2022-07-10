<template>
  <div class="row">
    <div class="col-sm-4 col-6 mb-4" v-for="(content, i) in contents" :key="i">
      <div class="card" style="width: 100%; border-radius: .75em;">
        <div class="gallery-file">
          <span class="material-icons icon-big">{{ icon }}</span>
        </div>
        <div class="card-body">
          <a :href="content.url" :download="content.name" class="content-center" target="blank">
            <span class="material-icons">file_download</span> {{ content.name }}
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    contents: {
      type: Array,
      default: () => []
    },
    icon: {
      default: 'article'
    }
  }
}
</script>

<style>
.gallery-file {
  width: 100%;
  height: 15em;
  border-radius: .75em .75em 0 0;
  background-image: linear-gradient(135deg, #ffe3b3, #53d2db);
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>