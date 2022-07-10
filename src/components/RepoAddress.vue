<template>
  <div class="hero">
    <h1 class="hero-text">GitleryHub</h1>
    <h3 class="hero-tagline">It should be a tagline, but i have no idea</h3>

    <div class="hero-input">
      <h3 class="font-white">Your GitHub Repo</h3>
      <div class="row">
        <div class="col-sm-10">
          <input
            type="text"
            class="form-control form-control-lg rounded-big mt-2"
            placeholder="ex: https://github.com/user/repo"
            v-model="url"
          />
        </div>
        <div class="col-sm-2">
          <button
            class="btn btn-lg btn-light fw-bold w-100 rounded-big mt-2"
            v-on:click="update"
          >
            Load
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import VsModal from '@vuesimple/vs-modal';

export default {
  props: {
    value: {
      default: "",
    },
  },
  components: {
    // VsModal,
  },
  data() {
    return {
      url: this.value,
    };
  },

  methods: {
    update() {
      console.log('update : ', this.url)
      // this.$refs["backdrop-modal"].open();
      this.$emit("submit", this.url);
    },
  },
};
</script>
<style>
.hero {
  padding: 10%;
  padding-top: 5%;
  padding-bottom: 2%;
  /* height: 100vh; */
  width: 100vw;
  background-image: linear-gradient(135deg, #53d2db, #4f8fbf);
  text-align: center;
}
.hero-text {
  font-weight: 800;
  font-size: 5rem;
  color: #fff;
}
.hero-tagline {
  /* color: #ffe3b3; */
  color: #26648b;
}
.hero-input {
  margin: 5% 0%;
}

@media (orientation: portrait) {
  .hero {
    padding-top: 10%;
    padding-bottom: 5%;
  }
  .hero-text {
    font-weight: 800;
    font-size: 3rem;
    color: #fff;
  }
  .hero-tagline {
    /* color: #ffe3b3; */
    color: #26648b;
  }
}
</style>
