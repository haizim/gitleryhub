<template>
  <div class="kosong">{{ message }}</div>
</template>

<script>
export default {
  props: {
    message: {
      default: "No repository yet",
    },
  },
};
</script>

<style>
.kosong {
  padding: 5%;
  border-radius: 1em;
  border: 5px dotted #aaa;
  color: #aaa;
  font-weight: bold;
  text-align: center;
  font-size: 2.5em;
}
</style>
