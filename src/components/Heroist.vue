<template>
  <div>
    <div class="list-view" >
      <h1 class="title">欢迎来到英雄峡谷</h1>
      <ul class="hero-list">
        <li class="hero" v-for="(hero,index) in list" :key="index">
          <img :src="hero.img" alt="" class="img" @click="gotoPlayer(hero)" />
          <p class="name">{{ hero.name }}</p> 
        </li>
      </ul>
    </div>

    <!-- <person id="1" v-show="personSeen" v-on:back="hidePerson"></person> -->
  </div>
</template>

<script>
import axios from "axios";
// import Person from "./Person";
export default {
  name: "Heroist",
  data() {
    return {
       list: [],
      // personSeen: false,

    };
  },
  created() {
    axios({
      url: "/data/data.json",
      method: "get",
    })
      .then((data) => {
        this.list = data.data;
      })
      
      .catch((err) => {
        console.log("error...", err);
      });
  },
  methods:{
   
    gotoPlayer(hero){
      this.$emit("switch",hero);
    }
     },
  components: {
    // Person,
  },
};
</script>

<style scoped>
.title {
  color: goldenrod;
  font-style: italic;
}
.hero-list {
  width: 60%;
  margin: 0 auto;
  display: flex;
  justify-content: space-around;
  list-style: none;
}
.hero .img {
  cursor: pointer;
  width: 87px;
  border: 2px solid rgb(32, 32, 218);
  border-top-left-radius: 15px;
  border-bottom-right-radius: 15px;
}
.hero .name {
  margin-top: 0;
}



</style>