<template>
  <div>
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item">Home</li>
        <li class="breadcrumb-item" v-for="(pth, index) in pathShow" :key="'pth-'+index">
          <span class="material-icons text-primary">navigate_next</span>{{ pth }}
        </li>
      </ol>
    </nav>
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
    },
    pathShow() {
      let pathNow = decodeURIComponent(this.path)
      pathNow = pathNow.split("/");
      pathNow.shift();

      return pathNow
    }
  }
}
</script>

<style>
.breadcrumb-item {
  display: inline-flex;
}
.breadcrumb-item + .breadcrumb-item::before {
  padding-right: 0;
  content: "";
}

.breadcrumb-item + .breadcrumb-item {
  padding-right: 0;
}
</style>
