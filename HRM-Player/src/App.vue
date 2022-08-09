<template>
  <div id="app">
    <!--IE报错   VIDEOJS: ERROR: (CODE:0 MEDIA_ERR_CUSTOM) FLASH: rtmpconnectfailure [object Object]
      谷歌火狐不支持flash-->
    <button id="rtmp" @click="change(1)">RTMP</button>
    <!-- 目前未使用MP4格式 -->
    <button id="mp4" @click="change(2)">MP4</button>
    <button id="hls" @click="change(3)">HLS</button>
    <button @click="pause">pause</button>
    <button @click="play">play</button>
    <button @click="reset">reset</button>
    <button id="full" @click="setFullScreen">setFullScreen</button>
    <hrm-player
      :width="900"
      :height="500"
      :muted="true"
      :autoplay="true"
      :controls="true"
      ref="myPlayer"
      @init="aaa"
      :source="src"
      :type="type"
    />
  </div>
</template>

<script>
import hrmPlayer from "../src/components/index.js";

export default {
  name: "App",
  components: {
    hrmPlayer,
  },
  data() {
    return {
      type: "",
      src: "",
    };
  },
  methods: {
    aaa(obj) {
      console.log("a", obj);
    },
    change(val) {
      console.log(val);
      switch (val) {
        case 1:
          // this.src = 'http://172.16.3.128:8080/live/test110.flv';
          this.src = "rtmp://172.16.3.128:1935/live/test110.flv";
          this.type = "rtmp/flv";
          break;
        case 2:
          this.src = "http://172.16.3.128:8080/live/test110.flv";
          this.type = "video/flv";
         //this.type = "video/mp4"; //原始
          break;
        case 3:
          this.src = "http://172.16.3.128:8080/hls/test110/playlist.m3u8";
          this.type = "application/x-mpegURL";
          break;
      }
    },
    pause() {
      this.$refs.myPlayer.pause();
    },
    play() {
      this.$refs.myPlayer.play();
    },
    reset() {
      this.$refs.myPlayer.reset();
    },
    setFullScreen() {
      this.$refs.myPlayer.setFullScreen();
    },
  },
};
</script>
