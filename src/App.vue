<template>
  <div id="app">
    <div class="header">
      <h1 class="h1">娜娜微原创</h1>
    </div>
    <div class="content">
      <el-carousel :interval="4000"
                   @change='carousel_trigger'
                   :autoplay="false"
                   arrow="never"
                   type="card"
                   height="775px"
                   v-show="!isVedioPlay">
        <el-carousel-item v-for="(work,index) in works"
                          :key="index">
          <img :src="work.coverImage"
               :style="initial_index == index ? '' : 'opacity: 0.75;'  "
               height="100%"
               width="auto"
               @click="coverImg(work.pid,work.v_url)" />
        </el-carousel-item>
      </el-carousel>
      <div v-show="isVedioPlay">
        <el-button type="danger"
                   @click="closeIframe"
                   size='mini'
                   style="position: fixed;"
                   plain>关闭
        </el-button>
        <iframe ref="myiframe"
                height=775
                width=100%
                autoplay='true'
                :src='playUrl'
                seamless
                isAutoPlay='true'
                frameborder=0
                allowfullscreen
                allownetworking=“internal”></iframe>
      </div>
      <div class="athor_info">
        <div class="athor"
             v-for="(item,index) in athor_info"
             :key="index">
          <p>片名：{{item.works_name}}</p>
          <p>主演：{{item.zhuyan}}</p>
          <p>导演：{{item.daoyan}}</p>
          <p>编剧：{{item.bianju}}</p>
          <p>摄像：{{item.shexiang}}</p>
          <p>后期：{{item.houqi}}</p>
        </div>
      </div>
      <el-row style="margin-top: 50px;">
        <el-col :span="24">
          <el-card :body-style="{ padding: '0px'}"
                   style=" background-color: transparent; border: 0">
            <img src="./static/img/woman.jpg"
                 class="image" />
            <div style="padding: 0.7467rem;">
              <div class="bottom clearfix">
                <time class="time">{{ currentDate }}</time>
                <el-button type="text"
                           class="button"
                           @click="isVisible = !isVisible">
                  联系作者</el-button>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>
    </div>
    <el-dialog :visible.sync='isVisible'
               title='联系作者'
               :modal='false'
               width="25%">
      <el-row>
        <el-col :span="6">QQ：</el-col>
        <el-col :span="6">2448745034</el-col>
      </el-row>
      <el-row>
        <el-col :span="6">VX：</el-col>
        <el-col :span="6">GL24487</el-col>
      </el-row>
    </el-dialog>
    <myFooter></myFooter>
  </div>
</template>

<script>
import myFooter from "@/components/Footer.vue";
export default {
  components: {
    myFooter
  },
  data () {
    return {
      initial_index: 0,//走马灯其实位置
      currentDate: new Date(), //拍摄时间,
      athor_info: [
        {
          id: 0,
          works_name: '天若有情',
          zhuyan: '梁婵娜',
          daoyan: '梅予馨',
          bianju: '陈娟 郭霜 梅予馨',
          shexiang: '陈娟 郭霜 但丽英',
          houqi: '陈娟'
        }
      ],//作者信息
      works: [
        { id: 0, coverImage: require('./static/img/tryq.jpg'), pid: '0', v_url: 'https://player.youku.com/embed/XNDY3NzcxNDQ5Ng==?rel=0&amp;autoplay=1' },
        { id: 1, coverImage: require('./static/img/tryq.jpg'), pid: '1', v_url: 'https://player.youku.com/embed/XNDY3NzcxNDQ5Ng==?rel=0&amp;autoplay=1' },
        { id: 2, coverImage: require('./static/img/tryq.jpg'), pid: '2', v_url: 'https://player.youku.com/embed/XNDY3NzcxNDQ5Ng==?rel=0&amp;autoplay=1' }
      ],// 作品信息
      isVedioPlay: false, // 视频播放
      playUrl: '', // 播放链接
      photos: [
        { id: '0', url: require('./static/img/woman.jpg') }
      ],// 相册
      isVisible: false, // 遮罩
      sizeObj: {
        height_tv: '30.6667rem',
        heigth_athor: '516px',
      } // 走马灯。图片高度
    };
  },
  methods: {
    // 走马灯
    carousel_trigger (event) {
      // console.log('走马灯event:', event);
      this.initial_index = event
    },
    // 手动走马灯
    setActiveItem () {
      // console.log('走马灯event:', event);
    },
    // 海报点击
    coverImg (e, v) {
      this.isVedioPlay = !this.isVedioPlay
      this.playUrl = v
      // console.log('imgStyContrl:', e, v);
    },
    // 关闭播放
    closeIframe () {
      this.isVedioPlay = !this.isVedioPlay
    }
  },
  created () {
    let user_agent = window.navigator.userAgent
    let device_regexp = /(iPhone|iPad|iPod|Android|WebOS|MeeGo|Windows Phone)/i
    if (device_regexp.test(user_agent)) {
      this.sizeObj.height_tv = '20.5333rem'
      this.sizeObj.heigth_athor = '5.92rem'
      console.log('1');
    }
  }
}
</script>
<style>
@font-face {
  font-family: myFont;
  src: url('./assets/font/I-Ngaan-2.ttf');
}

#app {
  font-family: myFont;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; 
  background-image: url("./static/img/bg3.gif");
  background-size: cover;
  background-position:center;
}

/* 头部动画 */
@-webkit-keyframes mymove {
    50% {box-shadow: 10px 20px 30px blue;}
}

/* Standard syntax */
@keyframes mymove {
    50% {box-shadow: 10px 20px 30px blue;}
}


.header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 20px;
  color: #FFFFFB;
  line-height: 96px;
  background-color: transparent;
    text-shadow: 0 0 20px #fdec84,
          10px -10px 30px #ffae35,
          20px -20px 40px #ec760c,
          -20px -60px 50px #cd4607,
          0px -80px 60px #973717,
          10px -40px 70px #451b0e;
  animation: mymove;
  -webkit-animation: mymove 5s infinite; /* Chrome, Safari, Opera */
}

.content {
  height: auto;
  padding: 0.2667rem 0;
  color: #FFFFFB;
  background-color: transparent;
}

.content .el-carousel__item h3 {
  color: #475669;
  font-size: 0.7467rem;
  opacity: 0;
  line-height: 10.6667rem;
  margin: 0;
}

.content .el-carousel__item:nth-child(2n) {
  background-color: transparent;
}

.content .el-carousel__item:nth-child(2n+1) { 
  background-color: transparent;
}

.athor_info {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 100%;
}

.athor {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  font-size: 18px;
  color: white;
  text-shadow: 0 0 20px #fdec84,
          10px -10px 30px #ffae35,
          20px -20px 40px #ec760c,
          -20px -60px 50px #cd4607,
          0px -80px 60px #973717,
          10px -40px 70px #451b0e;
}

.time {
  font-size: 0.6933rem;
  color: #999;
}

.bottom {
  margin-top: 0.6933rem;
  line-height: 0.64rem;
}

.button {
  padding: 0;
  float: right;
}

.image {
  width: 100%;
  height: auto;
  display: block;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
  background-color: transparent;
}

.clearfix:after {
  clear: both;
  background-color: transparent;
}

.el-carousel__item .el-carousel__mask {
  background-color: transparent;
}

</style>
