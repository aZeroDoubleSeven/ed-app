<template>
  <view>
    <u-navbar title="多音节测试题" :safeAreaInsetTop="true" placeholder fixed>
      <view @click="onBack" class="u-nav-slot" slot="left">
        <u-icon name="arrow-left" size="19"></u-icon>
      </view>
    </u-navbar>
    <view class="container">
      <view class="examination-wrap">
        <view class="section monosyllable">
          <view class="multisyllable-content">
            <view class="b" v-for="i in multisyllableList">
              <view class="w">{{ i }}</view>
            </view>
          </view>
        </view>

        <view class="tip">大声清晰朗读能活得更精准的分数哦</view>
      </view>
    </view>

    <view class="voice-wrap">
      <view class="count-down">
        <u-count-down :time="2 * 60 * 1000" format="mm:ss"></u-count-down>
      </view>

      <view class="voice-btn" @click="onRecord">
        <voiceui v-if="showVoiceUi" />
        <text v-if="!showVoiceUi">开始录制</text>
      </view>
      <view class="submit-btn" @click="onSubmit">提交</view>
    </view>

    <popup :show="show" @close="close" />
  </view>
</template>

<script>
const recorderManager = uni.getRecorderManager();
const innerAudioContext = uni.createInnerAudioContext();
innerAudioContext.autoplay = true;

import voiceui from "../../components/voiceui.vue";
import popup from "../../components/popup.vue";

export default {
  data() {
    return {
      showVoiceUi: false,
      show: false,
      model: "test",
      voicePath: "",
      multisyllableList: ["滋长", "滋长", "滋长", "滋长", "滋长"],
    };
  },
  components: { voiceui, popup },
  methods: {
    onSubmit() {
      this.toPage("/pages/article/article");
    },
    toPage(url) {
      if (url) {
        uni.navigateTo({
          url: url,
        });
      }
    },
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
    },
    confirm() {
      this.show = false;
    },
    OnExit() {
      this.show = false;
    },
    onRecord() {
      console.log("录音开始");
      this.showVoiceUi = true;
    },
    endRecord() {
      console.log("录音结束");
      // recorderManager.stop();
      this.showVoiceUi = false;
    },
    startRecord() {
      // console.log("开始录音");
      // recorderManager.start();
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
    // let self = this;
    // recorderManager.onStop(function (res) {
    //   console.log("recorder stop" + JSON.stringify(res));
    //   self.voicePath = res.tempFilePath;
    // });
  },
};
</script>

<style lang="scss" scoped>
.container {
  position: relative;
  margin-top: 40rpx;
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
    .multisyllable-content {
      box-sizing: border-box;
      padding: 0 12rpx;
      position: relative;
      width: 100%;
      height: auto;
      display: flex;
      flex-wrap: wrap;
      .b {
        width: 133rpx;
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

.voice-wrap {
  position: fixed;
  box-sizing: border-box;
  height: 90rpx;
  line-height: 90rpx;
  bottom: 0;
  width: 100%;
  z-index: 99;
  color: #ffffff;
  background-color: #1d74fb;
  display: flex;
  align-items: center;

  /deep/ .count-down {
    position: absolute;
    width: 156rpx;
    left: 28rpx;
    z-index: 99;
    .u-count-down__text {
      color: #ffffff;
      font-size: 28rpx;
    }
  }

  .voice-btn {
    width: 90%;
    text-align: center;
    color: #ffffff;
    font-size: 28rpx;
    letter-spacing: 4rpx;
  }

  .submit-btn {
    z-index: 99;
    position: absolute;
    width: 186rpx;
    text-align: center;
    right: 0;
    color: #ffffff;
    font-size: 28rpx;
    letter-spacing: 4rpx;
    border-left: 1rpx solid #ffffff;

    &:active {
      color: #ffffff;
      background: #024cbf;
    }
  }
}
</style>
