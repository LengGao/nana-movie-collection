<template>
  <div class="HelloWorld_Mobile">
    <div class="header">
      <span>娜娜原创</span>
    </div>
    <div class="content">
      <el-carousel @change='carousel_trigger'
                   :autoplay="false"
                   arrow="never"
                   type="card"
                   height="10.3333rem"
                   style="width: 100%;"
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
      <div v-if="isVedioPlay">
        <van-button type="danger"
                    @click="closeIframe"
                    style="position: fixed;"
                    plain
                    size='mini'>关闭</van-button>
        <iframe ref="myiframe"
                height='200'
                width=100%
                autoplay='true'
                :src='playUrl'
                seamless
                isAutoPlay='true'
                frameborder=0
                allowfullscreen
                allownetworking=“internal”></iframe>
      </div>
      <el-carousel @change='carousel_trigger'
                   ref="carousel"
                   :autoplay="false"
                   arrow="never"
                   type="card"
                   class="carousel_info"
                   style="width: 100%; height: 6.4rem; overflow: hidden;"
                   v-show="!isVedioPlay">
        <el-carousel-item v-for="(item,index) in athor_info"
                          :key="index">
          <div class="athor_info">
            <div class="athor">
              <span>片名：{{item.works_name}}</span>
              <span>主演：{{item.zhuyan}}</span>
              <span>导演：{{item.daoyan}}</span>
              <span>编剧：{{item.bianju}}</span>
              <span>摄像：{{item.shexiang}}</span>
              <span>后期：{{item.houqi}}</span>
            </div>
          </div>
        </el-carousel-item>
      </el-carousel>
      <el-row class="contact">
        <el-col :span="24">
          <el-card :body-style="{ padding: '0px'}"
                   style=" background-color: transparent; border: 0">
            <img src="@/static/img/woman.jpg"
                 class="image" />
            <div style="padding: 0.2667rem;">
              <div class="bottom clearfix">
                <time class="time">{{ currentDate }}</time>
                <el-button type="text"
                           class="bottom"
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
               width="80%">
      <el-row>
        <el-col :span="4">QQ：</el-col>
        <el-col :span="10">2448745034</el-col>
      </el-row>
      <el-row>
        <el-col :span="4">VX：</el-col>
        <el-col :span="10">GL24487</el-col>
      </el-row>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld-Mobile',
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
        },
        {
          id: 1,
          works_name: '天若有情',
          zhuyan: '梁婵娜',
          daoyan: '梅予馨',
          bianju: '陈娟 郭霜 梅予馨',
          shexiang: '陈娟 郭霜 但丽英',
          houqi: '陈娟'
        }, {
          id: 2,
          works_name: '天若有情',
          zhuyan: '梁婵娜',
          daoyan: '梅予馨',
          bianju: '陈娟 郭霜 梅予馨',
          shexiang: '陈娟 郭霜 但丽英',
          houqi: '陈娟'
        }
      ],//作者信息
      works: [
        { id: 0, coverImage: require('@/static/img/tryq.jpg'), pid: '0', v_url: 'https://player.youku.com/embed/XNDY3NzcxNDQ5Ng==?rel=0&amp;autoplay=1' },
        { id: 1, coverImage: require('@/static/img/tryq.jpg'), pid: '1', v_url: 'https://player.youku.com/embed/XNDY3NzcxNDQ5Ng==?rel=0&amp;autoplay=1' },
        { id: 2, coverImage: require('@/static/img/tryq.jpg'), pid: '2', v_url: 'https://player.youku.com/embed/XNDY3NzcxNDQ5Ng==?rel=0&amp;autoplay=1' }
      ],// 作品信息
      isVedioPlay: false, // 视频播放
      playUrl: '', // 播放链接
      photos: [
        { id: '0', url: require('@/static/img/woman.jpg') }
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
      this.setActiveItem(event)
    },
    // 手动走马灯
    setActiveItem (event) {
      this.$refs.carousel.setActiveItem(event)
      // console.log('setActiveItem:', event);
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
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  text-align: center;
    overflow: hidden;
}

@-webkit-keyframes mymove {
    50% {box-shadow: 0.2667rem 0.5333rem 0.8rem blue;}
}

@keyframes mymove {
    50% {box-shadow: 0.2667rem 0.5333rem 0.8rem blue;}
}

.header {
  font-size: 1.4933rem;
  line-height: 5.12rem;
  color: #FFFFFB;  
  background-color: transparent;
  text-shadow: 0 0 0.5333rem #fdec84,
      0.2667rem -0.2667rem 0.8rem #ffae35,
      0.5333rem -0.5333rem 1.0667rem #ec760c,
      -0.5333rem -1.6rem 1.3333rem #cd4607,
      0rem -2.1333rem 1.6rem #973717,
      0.2667rem -1.0667rem 1.8667rem #451b0e;
  animation: mymove;
  -webkit-animation: mymove 5s infinite;
}

.content {
  margin: 0.2667rem 0 0;
  color: #FFFFFB;
}

.carousel_info {
  height: 5.3333rem;
  margin: 0.5333rem 0 0;
}

.athor_info {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  height: 4.32rem;
  transform: translateY(10px)
}

.athor {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  font-size: 0.3733rem;
  text-shadow: 0 0 0.5333rem #fdec84,
          0.2667rem -0.2667rem 0.8rem #ffae35,
          0.5333rem -0.5333rem 1.0667rem #ec760c,
          -0.5333rem -1.6rem 1.3333rem #cd4607,
          0rem -2.1333rem 1.6rem #973717,
          0.2667rem -1.0667rem 1.8667rem #451b0e;
    transform: scale(0.9);
  -webkit-transform: scale(0.9); 
}

.image {
  display: block;
  width: 100%;
  height: auto;
}

.contact {
  margin-top: 0.5333rem;
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

.time {
  font: 0.32rem;
  color: #999;
  transform: scale(0.8);
  -webkit-transform: scale(0.8);
}

.bottom {
  margin-top: 0.2667rem;
  padding: 0;
  float: right;
  font: 0.32rem;
  line-height: 1.28rem;
  transform: scale(0.9);
  -webkit-transform: scale(0.9);
} 


</style>
<style>
.HelloWorld_Mobile .el-carousel__indicator--horizontal {
  padding: 0.32rem 0.1067rem;
}

.HelloWorld_Mobile .el-carousel__indicator--horizontal .el-carousel__button {
  width: 0.8rem;
  height: 0.0533rem;
}
</style>

