<template>
  <div
    class="modal fade"
    :class="{ 'show': isActive }"
    id="exampleModalLive"
    tabindex="-1"
    aria-labelledby="exampleModalLiveLabel"
    :style="isActive ? 'display: block' : 'display: none'"
    :aria-modal="isActive"
    role="dialog"
    @click="close"
  >
    <div class="modal-dialog modal-dialog-centered modal-lg">
      <div class="modal-content">
        <div class="modal-header">
          <p class="modal-title" id="exampleModalLabel">{{ title }}</p>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="close"></button>
        </div>
        <div class="modal-body">
          <slot></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    active: {
      type: Boolean,
      default: false
    },
    title: {
      default: ''
    }
  },
  data() {
    return {
      isActive: this.active
    }
  },
  methods: {
    close() {
      this.isActive = false
      this.$emit('submit', false)
    }
  },
  watch: {
    active: function(val) {
      this.isActive = val
    }
  }
}
</script>

<style>
.modal {
  background-color: rgba(25,25,25, .5);
}
</style>