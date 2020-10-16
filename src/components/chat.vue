<template>
  <div class="chat">
    <el-container class="chat-container">
      <el-header class="chat-header">
        <h3>机器人小冷，竭诚为您服务</h3>
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
        <el-input v-model="input" type="textarea" resize="none" size="medium "></el-input>
        <el-button @click="websocketsend" class="btn-send" type="primary" >发送</el-button>
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
      // const wsuri = "ws://121.40.165.18:8800";
      const wsuri = "ws://175.24.41.213:3010/";
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
  height: 16rem;
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
  height: 53px;
}
.info-self {
  text-align: right;
  color: #fff;
}
.info-other {
  text-align: left;
  color: #439EFf;
}
</style>