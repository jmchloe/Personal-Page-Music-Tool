<template>
  <div class="home">
   
    <Heroist v-show="!showPlayer1" @switch="showPlay"></Heroist>
    <!-- <player v-bind:hero="current" v-show="showPlayer1" @change="changeHero"></player> -->
    <player @change="changeHero" @back="showPlayer1=false" ref="playerId" :hero="current" v-show="showPlayer1"> </player>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios"
import Heroist from '@/components/Heroist.vue'
import Player from '../components/Player'
export default {
  name: 'Home',
  data(){
    return{    
      showPlayer1:false,
      current:{},
      list:[],
    }},
  components:{
    Heroist,
    Player
  },
  created(){
    axios({
      url:"/data/data.json",
      method:"get",
      data:{},
    })
    .then((data)=>{
       this.list=data.data;
      }) 
        .catch((err)=>{
            console.log("error...", err);
        });

  },
  methods:{
    showPlay(hero){
      this.current=hero;
      this.showPlayer1=true;
    },
    changeHero(flag){
      let list=this.list;
      let id= this.current.id;
      if(flag=="prev"){
        this.current=id==0?list[list.length-1]:list[id-1];
      }else{
        this.current=id==list.length-1?list[0]:list[id+1];

      }

    },
    gotoAbout(){
       this.$router.push("/about");
      
    }
  },
}
</script>
