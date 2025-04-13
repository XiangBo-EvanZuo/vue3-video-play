<template>
  <!-- <div style="height:150px; margin-top:100px">
    <d-slider v-model="options.volume"></d-slider>
  </div>-->
  <div style="text-align: center">
    <videoPlay ref="video" style="display: inline-block; width: 100%" v-bind="options" />
    <div>
      <div class="time-jump" @click="jumpTo(0)">00:00</div>
      <div class="time-jump" @click="jumpTo(10)">00:10</div>
      <div class="time-jump" @click="jumpTo(50)">00:50</div>
      <div class="time-jump" @click="jumpTo(70)">01:10</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref, nextTick } from "vue";
import { videoPlay } from "../lib/index.js";

const options = reactive({
  width: "100%",
  height: "450px",
  color: "#409eff",
  muted: false, //静音
  webFullScreen: false,
  autoPlay: false, //自动播放
  currentTime: 0,
  loop: false, //循环播放
  mirror: false, //镜像画面
  ligthOff: false, //关灯模式
  volume: 0.3, //默认音量大小
  control: true, //是否显示控制器
  title: "", //视频名称
  type: "m3u8",
  src: "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8", //视频源
  // src: "https://cdn.jsdelivr.net/gh/xdlumia/files/video-play/IronMan.mp4", //视频源
  // src: "https://logos-channel.scaleengine.net/logos-channel/live/biblescreen-ad-free/playlist.m3u8", //视频源
  poster: "https://cdn.jsdelivr.net/gh/xdlumia/files/video-play/ironMan.jpg", //封面
  controlBtns: [
    "audioTrack",
    "quality",
    "speedRate",
    "volume",
    "setting",
    "pip",
    "pageFullScreen",
    "fullScreen",
  ],
});
const video = ref(null);
const jumpTo = (time) => {
  video.value?.progressBarPosition(time)
}
nextTick(() => {
  console.log(video.value);
});
</script>

<style scoped>
/* 按钮容器 */
div {
  display: flex;
  gap: 15px;
  margin: 20px 0;
  flex-wrap: wrap;
}

/* 基础按钮样式 */
.time-jump {
  cursor: pointer;
  padding: 10px 25px;
  border-radius: 8px;
  background: linear-gradient(145deg, #2c3e50, #34495e);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #ecf0f1;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
}

/* 悬停效果 */
.time-jump:hover {
  background: linear-gradient(145deg, #34495e, #2c3e50);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

/* 点击效果 */
.time-jump:active {
  transform: translateY(1px);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

/* 点击波纹效果 */
.time-jump::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 5px;
  height: 5px;
  background: rgba(255, 255, 255, 0.3);
  opacity: 0;
  border-radius: 50%;
  transform: translate(-50%, -50%) scale(1);
  transition: all 0.5s ease-out;
}

.time-jump:active::after {
  width: 200px;
  height: 200px;
  opacity: 0.5;
  transition: 0s;
}

</style>