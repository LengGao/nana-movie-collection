<template>
  <div class="chat">
    <el-container class="chat-container">
      <el-header class="chat-header">
        <h5>机器人小冷，竭诚为您服务</h5>
      </el-header>
      <el-main class="chat-main">
        <span> {{new Date()}}</span>
        <div class="chat-content">
          <span v-for="(info,index) in infos" :key="index">
            <p>{{info.sendTime}}</p>
            <p :class="info.from === 'server' ? 'info-other': 'info-self' ">{{info.content}}</p>
          </span>
        </div>
      </el-main>
      <el-footer class="chat-footer">
        <el-input class="my-textarea" v-model="input" type="textarea" />
        <!-- <input class="my-textarea" v-model="input" type="textarea" />  -->
        <el-button @click="websocketsend" class="btn-send" type="primary" size="mini" >发送</el-button>
      </el-footer>
    </el-container>
  </div>
</template>
<script>
export default {
  data () {
    return {
      input: '',
      websock: null,
      // info: "hello",
      infos: [ 
      ]
    }
  },
  methods: {
    initWebSocket(){ //初始化weosocket
      const wsuri = "ws://nana-movie.top:8030/";
      this.websock = new WebSocket(wsuri);
      this.websock.onmessage = this.websocketonmessage;
      this.websock.onopen = this.websocketonopen;
      this.websock.onerror = this.websocketonerror;
      this.websock.onclose = this.websocketclose;
    },
    websocketonopen(){ //连接建立之后执行send方法发送数据
    },
    websocketonerror(){//连接建立失败重连
      this.initWebSocket();
    },
    websocketonmessage(e){ //数据接收
      const redata = JSON.parse(e.data);
      this.infos.push(redata)
      console.log("websocketonmessage",redata,this.infos)
    },
    websocketsend(){//数据发送
      var sendData = {
        from: 'client',
        sendTime: new Date(),
        contentType: 'text',
        content: this.input
      }
      this.infos.push(sendData);
      this.websock.send(JSON.stringify(sendData));
      console.log('websocketsend')
    },
    websocketclose(e){  //关闭
      console.log('断开连接',e);
    }
  },
  created () {
    this.initWebSocket();
  },
  destroyed() {
    this.websock.close() //离开路由之后断开websocket连接
  }
}
</script>

<style scoped>
.chat {
  margin-top: 0.2667rem;
}
.chat-container {
  height: 21.3333rem;
  background-color: #B3C0D1;
  color: #333;
}
.chat-header {
  border-bottom: #333 solid 1px;
}
.chat-main {
  padding: 0;
  overflow-y: scroll;
}
.chat-footer { 
  display: flex;
  flex-direction: row;
  align-items: flex-end;
  padding: 0;
}
.btn-send {
  position: absolute;
  right: 0;
  bottom: 0;
  height: 1.4933rem;
  margin-bottom: 0.1333rem;
}
.info-self {
  text-align: right;
  color: #fff;
}
.info-other {
  text-align: left;
  color: #439EFf;
}

.my-textarea {
    display: block;
    resize: none;
    padding-right: 24%;
    margin-bottom: 0.0533rem;
    line-height: 1.5;
    box-sizing: border-box;
    width: 100%;
    min-height: 1.4933rem;
    font-size: inherit;
    color: #606266;
    background-color: #FFF;
    background-image: none;
}
</style>