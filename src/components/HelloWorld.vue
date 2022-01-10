<template>
  <div class="hello">
    <iframe
      id="u3d-frame"
      name="u3d-frame"
      src="http://127.0.0.1:8081/"
      frameborder="0"
    ></iframe>
    <div class="btn-box">
      <button @click="toggleColor">切换颜色</button>
      <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
      <button @click="insertRandom">向number控件传递随机数</button>
      <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
      <button @click="insertText">向string控件传递一条文本消息</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      u3dFrame: null,
      times:0,
    };
  },
  mounted() {
    this.u3dFrame = document.getElementById("u3d-frame");
    // message 事件监听来自u3d窗口发来的消息
    window.addEventListener("message", function (event) {
      /* 接收消息并处理消息 */
      // console.log("message event", event);
      if (event.origin != "http://127.0.0.1:8081") {
        return;
      }
      window.console.log(
        `vue：message事件回调，方法名：${event.data.fnName}，参数：`
      );
      window.console.log(event.data.payload);

      // 模拟处理数据(2秒之后回传数据给 u3d窗口)
      window.setTimeout(() => {
        const payload = {
          height: 100,
          unitNum: 5,
          houserNum: 400,
          year: 2003,
          city: "北京",
          id: "longfor_888888",
        };
        const data = {
          cbName: "OnString",
          payload,
        };
        event.source.postMessage(data, "*");
      }, 1500);
    });
  },
  methods: {
    toggleColor() {
      const data = {
        cbName: "OnToggle",
        payload: null,
      };
      this.u3dFrame.contentWindow.postMessage(data, "*");
    },
    insertRandom() {
      const data = {
        cbName: "OnNumber",
        payload: Math.floor(Math.random() * 10 + 1),
      };
      this.u3dFrame.contentWindow.postMessage(data, "*");
    },
    insertText() {
      const data = {
        cbName: "OnString",
        payload: new Date().toString(),
      };
      this.u3dFrame.contentWindow.postMessage(data, "*");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}
#u3d-frame {
  width: 100%;
  height: 700px;
}
</style>
