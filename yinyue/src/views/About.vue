<template>
  <div class="about">
    <button class="back-btn" @click="goback">返回</button>
    <h1>当前机器号码{{ current }}</h1>
    <button class="timer-control" @click="changeTimer">{{ timerState }}</button>
    <img src="" alt="" class="photo" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: 0,
      timer: null,
      timerState: "停止",
    };
  },
  methods: {
    goback() {
      debugger;
      this.$router.go(-1);
    },
    changeTimer() {
      debugger
      this.timerState=this.timerState == "停止"?"开始": "停止";
      if(this.timerState=="停止"){
            this.timer = setInterval(() => {
      this.current = Math.round(Math.random() * 50);
    }, 100);
      }else{
    
        clearInterval(this.timer)

      }
       
    },
  },
  created() {
    console.log("params...", this.$route.params);
  },
  mounted() {
    this.timer = setInterval(() => {
      this.current = Math.round(Math.random() * 50);
    }, 100);
  },

  /* beforeRouteEnter (to, from, next) {
    console.log("to params...",to.params)
    console.log(from)
   next();
  } */
};
</script>

<style  scoped>
.about {
}
.back-btn {
  float: left;
  margin: 15px;
  width: 80px;
  height: 35px;
  background: rgb(32, 235, 32);
  color: white;
  font-weight: 600;
  border-radius: 5px;
  border: none;
  cursor: pointer;
}
.back-btn:hover {
  background: blueviolet;
}
.timer-control {
  width: 100px;
  height: 40px;
  margin: 100px auto;
  cursor: pointer;
}
</style>