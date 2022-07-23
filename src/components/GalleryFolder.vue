<template>
  <div class="row">
    <div class="col-sm-2 col-6"  v-for="(folder, i) in contents" :key="i">
      <button class="btn btn-light w-100 mb-2 content-center" @click="setPath(folder.path)">
        <span class="material-icons">
          <template v-if="folder.path == '' && folder.name == 'home'">
            cottage
          </template>
          <template v-else-if="folder.path == back && folder.name == 'back'">
            arrow_back
          </template>
          <template v-else>
            folder
          </template>
        </span> 
        {{ folder.name }}
      </button>
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
    path: {
      type: String,
      default: ""
    }
  },
  methods: {
    setPath(val) {
      this.$emit('submit', val)
    }
  },
  computed: {
    back() {
      let kembali = this.path.split('/')
      kembali.pop()

      return kembali.join('/')
    }
  }
}
</script>