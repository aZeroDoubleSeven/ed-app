<template>
  <view>
    <u-navbar title="朗读短文" :safeAreaInsetTop="true" placeholder fixed>
      <view @click="onBack" class="u-nav-slot" slot="left">
        <u-icon name="arrow-left" size="19"></u-icon>
      </view>
    </u-navbar>
    <view class="container">
      <view class="examination-wrap">
        <view class="section monosyllable">
          <rich-text :nodes="articleContent"></rich-text>
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
      articleContent: `我常常遗憾 终有一日，村子里来了一个天文学家。他在我家门前路过，突然发现了这块石头，眼光立即就拉直了。他再没有走去，就住了下来：以后又来了好些人，都说这是一块陨石，从天上落下来已经有二三百年了，是一件了不起的东西，不久便来了车，小心翼翼地将它运走了。我家门前那块丑石呢：它黑黝黝地卧在那里，牛似的模样：谁也不知道是什么时候留在这里的，谁也不去理会它。只是麦收时节，门前摊了麦子，奶奶总是要说：“这块丑石，多碍地面哟，啥时把它搬走吧。 它不像汉白玉那样的细腻，可以凿下刻字雕花；也不像大青石那样的光滑，可以供来浣纱捶布。它静静地卧在那里，院边的槐荫没有庇覆它，花儿也不再在它身边生长，荒草便繁衍出来，枝蔓上下。慢慢地，它竟锈上了绿苔、黑斑。我们这些做孩子的，也讨厌起它来，曾合伙要搬走它，但力气又不足：虽时时咒骂它，嫌弃它，也无可奈何，只好任它留在那里去了。这使我们都很惊奇！这又怪又丑的石头，原来是天上的呢！它补过天，在天上发过热、闪过光，我们的先祖或许仰望过它，它给了他们光明、向往、憧憬；而它落下来了。在污土里，荒草里，一躺就是几百年了！`,
    };
  },
  components: { voiceui, popup },
  methods: {
    onSubmit() {
      this.toPage("/pages/titles/titles");
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
