<template>
  <div id="app" style=" overflow: hidden;">
    <HelloWorldMobile v-if="user_agent" />
    <HelloWorld v-else />
    <myFooter />
  </div>
</template>

<script>
import myFooter from "@/components/Footer.vue";
import HelloWorld from "@/components/HelloWorld.vue";
import HelloWorld_Mobile from "@/components/HelloWorld-Mobile.vue";
export default {
  components: {
    myFooter,
    HelloWorld,
    'HelloWorldMobile': HelloWorld_Mobile
  },
  data () {
    return {
      user_agent: false
    }
  },
  created () {
    let user_agent = window.navigator.userAgent
    let device_regexp = /(iPhone|iPad|iPod|Android|WebOS|MeeGo|Windows Phone)/i
    // if (device_regexp.test(user_agent)) {
    //   this.sizeObj.height_tv = '769.9987px'
    //   this.sizeObj.heigth_athor = '222px'
    // }
    //   console.log('1');  
    return this.user_agent = device_regexp.test(user_agent)
  }
}
</script>
<style>

body {
  width: 100vw;
  overflow-x: hidden;
}

@font-face {
  font-family: myFont;
  src: url('./assets/font/I-Ngaan-2.ttf');
}

#app {
  font-family: myFont;
  -webkit-font-smoothing: myFont;
  -moz-osx-font-smoothing: myFont;
  text-align: center;
  color: #2c3e50; 
  background-image: url("./static/img/bg3.gif");
  background-size: 100% auto;
}

.el-carousel__item .el-carousel__mask {
  background-color: transparent;
}
</style>
