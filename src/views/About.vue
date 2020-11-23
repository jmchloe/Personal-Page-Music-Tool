<template>
  <div class="about">

  <button class="back-btn" @click="goback" >返回</button>
    <h1>这是一个学生的主页</h1>
    <img  class="photo" v-bind:src="info.photo" alt="" >
    <div class="name"><strong>{{ info.name }}</strong></div>
    <div class="age"><b>{{ info.age }}</b></div>
    <div class="Class"><b>{{ info.Class }}</b></div>

  </div>
</template>
<script>
import axios from "axios";
export default {
  data(){
    return{
      info:{

      },
     
    };
  },
  methods:{
    goback(){
      this.$router.go(-1)
    },
  },
  watch:{
    $route(to,from){
      alert(to.params.id)
      console.log(from)
    }
  },
    created(){
      // console.log("ssss",this.$route.params),
      axios({
      url: "/data/me.json",
      method: "get",
    })
      .then((me) => {
        this.info = me.data;
      })
      .catch((err) => {
        console.log("error...", err);
      });
  },
   
  // beforeRouteEnter (to, from, next) {
  //   console.log("xxxxx",to.params)
  //   console.log(from)
  //   next();
  // }


};
</script>
<style scoped>
.about{
  background: linear-gradient(40deg,#152ae4,red,rgba(94, 15, 221, 0.801)); 
  float: center;
  height: 500px;
  width: 100%;
  position :absolute;

}
.back-btn{
  
  margin: 50px;
  width: 50px;
  height: 30px;
  background: #f0ff67;
  color: grey;
  border: rgb(130, 21, 219);
  padding:rgba(42, 127, 238, 0.801);
  border-radius:10px 10px 10px 10px;
  position: relative;
 
  
  
}

.photo{
  float:center;
  margin: 0 auto;
  width: 100px;
  height: 100px;
  border-radius:60px 60px 60px 60px;
  border: 5px solid rgb(33, 33, 70);
  

}
.name+.Class+.age{
   text-align: center;
   
   
}
/*.name{
  text-align: center;
}
.Class{
   text-align: center;
}
.age{
   text-align: center;
}
*/
</style>