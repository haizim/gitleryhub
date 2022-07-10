<template>
  <div class="row">
    <div class="col-sm-2 col-6"  v-for="(folder, i) in contents" :key="i">
      <button class="btn btn-light w-100 mb-2 content-center" @click="setPath(folder.path)">
        <span class="material-icons">
          folder
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
    }
  },
  methods: {
    setPath(val) {
      this.$emit('submit', val)
    }
  }
}
</script>