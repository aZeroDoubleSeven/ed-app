<template>
  <view>
    <u-navbar title="单音节测试题" :safeAreaInsetTop="false">
      <view @click="onBack" class="u-nav-slot" slot="left">
        <u-icon name="arrow-left" size="19"></u-icon>
      </view>
    </u-navbar>
    <view class="container">
      <view class="examination-wrap">
        <view class="section monosyllable">
          <view class="monosyllable-content">
            <view class="b" v-for="i in monosyllableList">
              <view class="w">{{ i }}</view>
            </view>
          </view>
        </view>

        <view class="tip">大声清晰朗读能活得更精准的分数哦</view>
      </view>
    </view>

    <view>
      <button @tap="startRecord">开始录音</button>
      <button @tap="endRecord">停止录音</button>
      <button @tap="playVoice">播放录音</button>
    </view>

    <u-popup :show="show" @close="close" @open="open" round="10">
      <view class="popup-style"> </view>
    </u-popup>
  </view>
</template>

<script>
const recorderManager = uni.getRecorderManager();
const innerAudioContext = uni.createInnerAudioContext();
innerAudioContext.autoplay = true;
export default {
  data() {
    return {
      show: false,
      model: "test",
      voicePath: "",
      monosyllableList:
        "的去太天涯是啊从弹出层容器用于展示弹窗信息提示等内容支持上下左右和中部弹出组件只提供容器内部内容由用户自定义吧你吗啊是的发给和",
    };
  },
  methods: {
    open() {
      this.show = true;
    },
    close() {
      this.show = false;
    },
    handlerRandom() {
      this.close();
    },
    setSubject(item) {
      this.title = item.name;
      this.close();
    },
    onBack() {
      this.open();
      // uni.navigateBack({
      //   animationType: "pop-out",
      //   animationDuration: 300,
      // });
    },
    confirm() {
      this.show = false;
    },
    OnExit() {
      this.show = false;
    },
    startRecord() {
      console.log("开始录音");

      recorderManager.start();
    },
    endRecord() {
      console.log("录音结束");
      recorderManager.stop();
    },
    playVoice() {
      console.log("播放录音");

      if (this.voicePath) {
        innerAudioContext.src = this.voicePath;
        innerAudioContext.play();
      }
    },
  },
  onLoad() {
    let self = this;
    recorderManager.onStop(function (res) {
      console.log("recorder stop" + JSON.stringify(res));
      self.voicePath = res.tempFilePath;
    });
  },
};
</script>

<style lang="scss" scoped>
.container {
  position: relative;
  margin-top: 128rpx;
  padding: 0 28rpx;
  .examination-wrap {
    .section {
      margin-bottom: 50rpx;
      .title {
        color: #444444;
        font-size: 32rpx;
        height: 32rpx;
        line-height: 32rpx;
        margin-bottom: 32rpx;
      }
    }
    .monosyllable-content {
      box-sizing: border-box;
      padding: 0 12rpx;
      position: relative;
      width: 100%;
      height: auto;
      display: flex;
      flex-wrap: wrap;
      .b {
        width: 66rpx;
        height: 66rpx;
        box-sizing: border-box;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 1rpx solid #999999;
        margin: -1rpx;
      }
      .w {
        color: #444444;
        font-size: 28rpx;
      }
    }

    .tip {
      text-align: center;
      color: #999999;
      line-height: 20rpx;
      height: 20rpx;
      font-size: 20rpx;
    }
  }
}

.popup-style {
  position: relative;
  width: 100%;
  height: 400rpx;
  border-radius: 10rpx;
}
</style>
