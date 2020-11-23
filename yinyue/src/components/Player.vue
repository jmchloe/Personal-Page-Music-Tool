<template>
  <div class="bg">
    <img class="photo" :src="hero.img" alt="" @click="back" />
    <audio :src="hero.music" controls loop></audio>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["hero"],
  data() {
    return {  };
  },

  methods: {
    back() {
      this.$emit("back", "hello!");
    },
  },
};
</script>

<style scoped>
.bg {
  background: linear-gradient(45deg, #990033, #3300ff);
  position: fixed;
  width: 100%;
  height: 100%;
}
.photo {
  width: 200px;
  margin-top: 100px;
  border-radius: 50%;
  animation: spin 10s linear infinite;
}
@keyframes spin {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>