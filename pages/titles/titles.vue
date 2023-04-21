<template>
  <view>
    <u-navbar title="命题说话" :safeAreaInsetTop="true" placeholder fixed>
      <view @click="onBack" class="u-nav-slot" slot="left">
        <u-icon name="arrow-left" size="19"></u-icon>
      </view>
    </u-navbar>
    <view class="container">
      <view class="examination-wrap titles">
        <view class="box option" v-if="step === 0">
          <view class="top">选择其中一个题目进行3分钟自由对话</view>
          <view class="opt-wrap">
            <view
              class="item"
              @click="onSelect(item)"
              v-for="(item, index) in titlesList"
              >{{ index + 1 }}. {{ item }}
              <u-icon class="icons" name="arrow-right"></u-icon>
            </view>
          </view>
        </view>
        <view class="box result" v-if="step === 1">
          <view class="top"> 请开始3分钟自由说话 </view>
          <view class="res">《{{ currentTitle }}》</view>
        </view>
        <view class="tip">
          <view style="margin-bottom: 20rpx">答题指南:</view>
          <view
            >1.答题开头建议为：<text style="color: #fe5f57"
              >我说话的题目是××</text
            ></view
          >
          <view>2.请说满3分钟，如果有效时长过短会影响分数</view>
          <view>3.注意保持音量适中，音量过小可能会影响分数</view>
        </view>
      </view>
    </view>

    <view class="voice-wrap">
      <view class="count-down">
        <u-count-down
          v-if="step === 1"
          :time="3 * 60 * 1000"
          format="mm:ss"
        ></u-count-down>
      </view>

      <view class="voice-btn" @click="onRecord">
        <voiceui v-if="showVoiceUi" />
        <text v-if="!showVoiceUi">开始录制</text>
      </view>

      <view
        class="submit-btn"
        :class="[step === 0 ? 'disabled' : '']"
        @click="onSubmit"
        >提交</view
      >
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
      step: 0,
      showVoiceUi: false,
      show: false,
      model: "test",
      voicePath: "",
      currentTitle: "",
      titlesList: ["我的学习生活", "难忘的旅行"],
    };
  },
  components: { voiceui, popup },
  methods: {
    onSubmit() {
      if (this.step === 1) {
        this.toPage("/pages/report/report");
      }
    },

    onSelect(title) {
      this.currentTitle = title;
      this.step = 1;
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
  padding: 0 56rpx;
  .examination-wrap {
    margin-bottom: 50rpx;

    .tip {
      text-align: left;
      view {
        color: #999999;
        line-height: 24rpx;
        height: 24rpx;
        font-size: 24rpx;
        margin-bottom: 14rpx;
      }
    }

    .box {
      position: relative;
      margin-bottom: 50rpx;
      .top {
        line-height: 32rpx;
        font-size: 32rpx;
        height: 32rpx;
        margin-bottom: 39rpx;
        color: #444444;
      }
    }

    .option {
      .opt-wrap {
        position: relative;
        display: flex;
        flex-direction: column;
        .item {
          position: relative;
          box-sizing: border-box;
          width: 100%;
          height: 72rpx;
          border-radius: 20rpx;
          line-height: 72rpx;
          font-size: 32rpx;
          padding: 0 20rpx;
          text-align: left;
          margin-bottom: 24rpx;
          color: #ffffff;
          background-color: #1d74fb;
          &:last-child {
            margin-bottom: 0rpx;
          }

          &:active {
            background-color: #024cbf;
          }

          /deep/ .icons {
            position: absolute;
            right: 30rpx;
            transform: translateY(-50rpx);
            .u-icon__icon {
              color: #ffffff !important;
            }
          }
        }
      }
    }

    .result {
      .res {
        height: 32rpx;
        line-height: 32rpx;
        font-size: 32rpx;
        color: #444444;
      }
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
    width: calc(100% - 186rpx);
    text-align: center;
    color: #ffffff;
    background-color: #1d74fb;
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

  .disabled {
    background-color: #999999 !important ;
    &:active {
      color: #ffffff;
      background: #999999 !important;
    }
  }
}
</style>
