<template>
  <div>
    <div class="list-view">
      <h1 class="title">欢迎来到英雄峡谷</h1>
      <ul class="hero-list">
        <li class="hero" v-for="hero in list" :key="hero.id">
          <img :src="hero.img" alt="" class="img" @click="gotoPlayer(hero)" />
          <p class="name">{{ hero.name }}</p>
        </li>
      </ul>
    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HeroList",
  data() {
    return {
      list: []
    };
  },
  created() {
    axios({
      url: "/data/data.json",
      method: "get",
      data:{}
    })
      .then((data) => {
        let list=data.data;
        list.forEach(item=>{
          item.music=`/music/${item.music}.mp3`;
        });
        this.list = data.data;
      })
      .catch((err) => {
        console.log("error...", err);
      });
  },
  mounted(){

  },
  methods:{
     gotoPlayer(hero){
      this.$emit("switch",hero);
     }
  },
  components: {
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
  width: 87px;
  border: 2px solid rgb(32, 32, 218);
  border-top-left-radius: 15px;
  border-bottom-right-radius: 15px;
}
.hero .img:hover{
  cursor: pointer;
}
.hero .name {
  margin-top: 0;
}
</style>