<template>
  <div id="card">
    <div class="box1">
      <p class="p1">{{ card.type }}</p>
      <h4>{{ card.title }}</h4>
      <p class="p2">{{ card.author }}</p>
      <p class="p3">{{ card.text }}</p>
      <div style="margin-bottom:10px;border-radius: 10px; overflow:hidden;box-shadow:1px 1px 2px #dadada">
          <img v-bind:src="card.imgSrc" width="20%" alt="" style="float:left"/>
          <div style="float:left">
              <p style="margin:5px">夏天的风</p>
              <p style="margin:10px 5px" class="p2">火车瞌睡了</p>
          </div>
          <van-icon v-bind:name="music[1]" v-show="toggole" style="  display: block;font-size: 16px;height: 71px; line-height: 71px; float: right;padding-right: 30px;"  @click="on()"/>
          <van-icon v-bind:name="music[0]" v-show="!toggole" style="  display: block;font-size: 16px;height: 71px; line-height: 71px; float: right;padding-right: 30px;" @click="off()" />
      </div>
    </div>
    <div class="bottomBar p2">
      <span>{{ card.date }}</span>
      <span class="right">
        <van-icon
          class="icon"
          name="like-o"
         v-bind:color="card.color"
          @click="like()"
        />
        <span>{{ card.num }}</span>
        <van-icon class="icon" name="more-o"  @click="showPopup()"/>
        <van-popup v-model="show"  position="bottom" :style="{ height: '30%'}" style=" text-align: center;font-size:20px" >
            <div class="middle">
                <p class="share"><van-icon v-bind:name="imgSrc[0]" /></p>
                <p class="share"><van-icon v-bind:name="imgSrc[1]" /></p>
                <p class="share"><van-icon v-bind:name="imgSrc[2]" /></p>
                <p class="share"><van-icon v-bind:name="imgSrc[3]" /></p>
            </div>
        </van-popup>
      </span>
    </div>
  </div>
</template>

<script>
export default {
    data(){
         return {
              show: false,
              toggole: true,
              music:[require('../assets/on.png'),require('../assets/off.png')],
              imgSrc: [
                require("../assets/icon01.png"),
                require("../assets/icon02.png"),
                require("../assets/icon03.png"),
                require("../assets/icon04.png"),
              ]
         }
    },
  props: {
    card: Object,
  },
  methods: {
    like: function() {
      if (this.card.color == "") {
        this.card.color = "#DC143C";
        this.card.num ++;
      } else {
        this.card.color = "";
        this.card.num --;
      }
    },
    showPopup() {
      this.show = true;
    },
    on(){
        this.toggole = false;
    },
    off(){
        this.toggole = true;
    }
  },
};
</script>

<style scoped>
.bottomBar {
  padding: 0 10px;
}
#card {
  margin-top: 5px;
  padding: 10px;
  background-color: #fff;
}
#card .img {
  border-radius: 10px;
  box-shadow: 1px 1px 5px #dadada;
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
}
#card .p1 {
  font-size: 12px;
  color: gray;
  text-align: center;
}
#card .p2 {
  font-size: 12px;
  color: gray;
}
#card .p3 {
  font-size: 14px;
  color: black;
}
.right {
  float: right;
}
.icon {
  margin-left: 40px;
}
.middle{
    position: relative;
    top: 50%; /*偏移*/
    transform: translateY(-50%);
}
.share{
    margin: 0;
    padding: 10px
}
</style>
