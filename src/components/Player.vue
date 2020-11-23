<template>
    <div class="bg">
    <!-- <button class="back-btn"></button> -->
        <img class="photo" v-bind:src="hero.img" alt="" @click="back">
        <audio v-bind:src="hero.music" loop id="audioId"></audio>
        <div class="control-bar">
           <span class="glyphicon glyphicon-fast-backward" @click="prev"></span> 
           <span :class="['glyphicon', playIcon]" @click="play"></span>
           <span class="glyphicon glyphicon-fast-forward" @click="next"></span>

        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    props:{
        hero:{} 
        },
    data(){
        return{
            animationState:{
                animationPlayState:"paused",
            },
            playIcon:"glyphicon-play",
        };
    },
    created(){
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
        back(){
            if (this.animationState.animationPlayState == "running") this.play();
            this.$emit("back","hello!")
        },
        play(){
            let paused = this.animationState.animationPlayState=="paused";
            this.animationState.animationPlayState=paused?"running":"paused";
            this.playIcon=paused?"glyphicon-pause":"glyphicon-play";
            paused?
            document.getElementById("audioId").play():
            document.getElementById("audioId").pause();
        },
        prev(){
         this.$emit("change","prev");
        // let list=this.list;
        // let id=this.hero.id;
        // let item=id==0?list[list.length-1]:list[id-1];

        // this.hero.id=item.id;
        // this.hero.img=item.img;
        // this.hero.music=item.music;


    },
    next(){
        // let list=this.list;
        // let id=this.hero.id;
        // let item=id==list[list.length-1]?list[0]:list[id+1];
        // this.hero.id=item.id;
        // this.hero.img=item.img;
        // this.hero.music=item.music;
        this.$emit("change","next");
    },
    },
    
};
</script>

<style scoped>
    .bg{
        background: linear-gradient(45deg, #990033, #3300FF);
        position: fixed;
        width: 100%;
        height: 100%;
    }
    .photo{
        width:200px;
        height: 200px;
        border-radius:80%;
        margin: 40px;
        animation: spin 8s linear infinite;
        animation-play-state:running ;
    }
    @keyframes spin {
        from{
            transform: rotate(0);
        }
        to{
          transform: rotate(360deg);

        }
    }
    
.control-bar{
    width: 500px;
    background: #fff;
    padding: 15px ;
    margin: 50px auto;
    border-radius: 15px;
    display: flex;
    justify-content: space-around;
}
.control-bar span{
    padding: 10px;
}
.control-bar span:hover{
    cursor: pointer;
    color:blueviolet;
}

</style>