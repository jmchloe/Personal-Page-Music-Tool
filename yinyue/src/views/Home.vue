<template>
  <div class="home">
    <hero-list v-show="!playerVisible" @switch="showPlayer"></hero-list>
    <player :hero="current" v-show="playerVisible"></player>
  </div>
</template>

<script>
// @ is an alias to /src
import HeroList from "@/components/HeroList.vue";
import Player from "../components/Player";
export default {
  name: "Home",
  data() {
    return {
      playerVisible: false,
      current: {},
    };
  },
  components: {
    HeroList,
    Player,
  },
  methods: {
    showPlayer(hero) {
      this.current = hero;
      this.playerVisible = true;
    },
    gotoAbout() {
      /* this.$router.push({
        name:"About",
        params:{
          id:25
        }
      }); */
      this.$router.push("/about/xiaoming");
    },
  },
};
</script>
