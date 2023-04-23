<template>
  <view>
    <u-navbar :title="title" :safeAreaInsetTop="true" placeholder fixed>
      <view @click="onBack" class="u-nav-slot" slot="left">
        <u-icon name="arrow-left" size="19"></u-icon>
      </view>
    </u-navbar>
    <view class="container">
      <view class="info-wrap">
        <view class="total"> 83.63 </view>
        <view class="more">
          <view class="t-socre">上次训练所得分:80.01分</view>
          <view class="b-tiem">上次训练时长为4分钟</view>
        </view>
      </view>

      <view class="examination-wrap">
        <!-- 单音节 -->
        <view class="section monosyllable">
          <view class="title"
            >本次错别字43个

            <view class="tips">
              <view class="err">红色错读</view>
              <view class="war">橘色不准</view>
            </view>
          </view>
          <view class="monosyllable-content">
            <view class="b" v-for="i in monosyllableList">
              <view class="w">{{ i }}</view>
            </view>
          </view>
        </view>

        <!-- 多音节 -->
        <view class="section multisyllable">
          <view class="title"
            >本次错别字43个
            <view class="tips">
              <view class="err">红色错读</view>
              <view class="war">橘色不准</view>
            </view>
          </view>
          <view class="multisyllable-content">
            <view class="b" v-for="i in multisyllableList">
              <view class="w">{{ i }}</view>
            </view>
          </view>
        </view>

        <view class="section article-content" v-if="false">
          <view class="title"
            >三、朗读短文
            <view class="tips">
              <view class="err">红色错读</view>
              <view class="war">橘色不准</view>
              <view class="score">81.83分</view>
            </view>
          </view>
          <rich-text class="article" :nodes="articleContent"></rich-text>
        </view>

        <view class="section titles" v-if="false">
          <view class="title"
            >四、命题说话
            <view class="tips">
              <view class="err">红色错读</view>
              <view class="war">橘色不准</view>
              <view class="score">81.83分</view>
            </view>
          </view>
          <view class="titles-content">
            <view class="item" v-for="(i, index) in titleList">
              {{ index + 1 }}. {{ i }}
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

  <script>
export default {
  data() {
    return {
      title: "训练报告",
      show: false,
      subjectLists: [
        { name: "模拟考试题1", status: false, score: "" },
        { name: "模拟考试题2", status: true, score: "98.9" },
        { name: "模拟考试题3", status: false, score: "" },
        { name: "模拟考试题4", status: false, score: "" },
        { name: "模拟考试题5", status: true, score: "98.9" },
        { name: "模拟考试题6", status: false, score: "" },
        { name: "模拟考试题7", status: false, score: "" },
        { name: "模拟考试题8", status: true, score: "98.9" },
        { name: "模拟考试题9", status: false, score: "" },
        { name: "模拟考试题10", status: false, score: "" },
        { name: "模拟考试题11", status: true, score: "98.9" },
        { name: "模拟考试题12", status: false, score: "" },
      ],
      monosyllableList: "的去太天涯是啊从吧你吗啊是的发给和",
      multisyllableList: [
        "滋长",
        "滋长",
        "滋长",
        "滋长",
        "滋长",
        "滋长",
        "滋长",
        "滋长",
        "滋长",
      ],
      articleContent: `我常常遗憾 终有一日，村子里来了一个天文学家。他在我家门前路过，突然发现了这块石头，眼光立即就拉直了。他再没有走去，就住了下来：以后又来了好些人，都说这是一块陨石，从天上落下来已经有二三百年了，是一件了不起的东西，不久便来了车，小心翼翼地将它运走了。我家门前那块丑石呢：它黑黝黝地卧在那里，牛似的模样：谁也不知道是什么时候留在这里的，谁也不去理会它。只是麦收时节，门前摊了麦子，奶奶总是要说：“这块丑石，多碍地面哟，啥时把它搬走吧。 它不像汉白玉那样的细腻，可以凿下刻字雕花；也不像大青石那样的光滑，可以供来浣纱捶布。它静静地卧在那里，院边的槐荫没有庇覆它，花儿也不再在它身边生长，荒草便繁衍出来，枝蔓上下。慢慢地，它竟锈上了绿苔、黑斑。我们这些做孩子的，也讨厌起它来，曾合伙要搬走它，但力气又不足：虽时时咒骂它，嫌弃它，也无可奈何，只好任它留在那里去了。这使我们都很惊奇！这又怪又丑的石头，原来是天上的呢！它补过天，在天上发过热、闪过光，我们的先祖或许仰望过它，它给了他们光明、向往、憧憬；而它落下来了。在污土里，荒草里，一躺就是几百年了！`,
      titleList: ["我最尊敬的人", "我的朋友"],
    };
  },
  methods: {
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
      uni.switchTab({
        url: "/pages/index/index",
      });
    },
    confirm() {
      this.show = false;
    },
    OnExit() {
      this.show = false;
    },
  },
};
</script>

  <style lang="scss" scoped>
.container {
  position: relative;
  margin-top: 40rpx;
  padding: 0 28rpx;
  .info-wrap {
    position: relative;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    width: 100%;
    height: 150rpx;
    padding: 24rpx 48rpx;
    border-radius: 20rpx;
    margin-bottom: 40rpx;
    box-shadow: 0px 2rpx 10rpx 1rpx rgba(0, 0, 0, 0.1);
    background-color: #1d74fb;

    .total {
      width: 100rpx;
      height: 100rpx;
      line-height: 100rpx;
      font-size: 32rpx;
      color: #444444;
      border-radius: 50%;
      text-align: center;
      background: #ffffff;
      margin-right: 32rpx;
    }

    .more {
      display: flex;
      flex-direction: column;
      .t-socre {
        height: 28rpx;
        line-height: 28rpx;
        font-size: 28rpx;
        margin-bottom: 16rpx;
        color: #ffffff;
      }

      .b-tiem {
        height: 20rpx;
        line-height: 20rpx;
        font-size: 20rpx;
        color: #ffffff;
      }
    }
  }

  .examination-wrap {
    padding-bottom: 20rpx;
    .section {
      margin-bottom: 40rpx;
      .title {
        position: relative;
        color: #999999;
        font-size: 20rpx;
        height: 20rpx;
        line-height: 32rpx;
        margin-bottom: 32rpx;

        .tips {
          position: absolute;
          display: flex;
          width: auto;
          left: 220rpx;
          top: 0;
          .err,
          .war {
            // box-sizing: border-box;
            width: 124rpx;
            height: 32rpx;
            line-height: 32rpx;
            font-size: 20rpx;
            text-align: center;
            background: #ffffff;
            border-radius: 29rpx;
          }
          .err {
            border: 1rpx solid #ff5e57;
            color: #ff5e57;
            margin-right: 18rpx;
          }

          .war {
            border: 1rpx solid #febc2e;
            color: #febc2e;
            margin-right: 16rpx;
          }

          .score {
            color: #999999;
            font-size: 20rpx;
          }
        }
      }
    }
    .monosyllable-content,
    .multisyllable-content {
      box-sizing: border-box;
      padding: 16rpx 12rpx;
      position: relative;
      width: 100%;
      height: auto;
      display: flex;
      flex-wrap: wrap;
      background-color: #ffffff;
      border-radius: 20rpx;

      .b {
        width: 110rpx;
        height: 94rpx;
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
    .multisyllable-content {
      .b {
        width: 133rpx;
        height: 100rpx;
      }
    }
    .article {
      box-sizing: border-box;
      font-size: 28rpx;

      div {
        padding: 16rpx;
        border: 1rpx solid #999999;
      }

      /deep/ .u-read-more__content {
        font-size: 28rpx;
        color: #444444;
      }
    }

    .titles {
      margin-bottom: 40rpx;
    }

    /deep/ .u-read-more__toggle {
      background-image: linear-gradient(
        -180deg,
        rgba(255, 255, 255, 0) 0%,
        rgba(248, 248, 248, 1) 80%
      ) !important;
    }
  }
}

.options-btn-wrap {
  position: fixed;
  height: 90rpx;
  line-height: 90rpx;
  bottom: 0;
  width: 100%;
  z-index: 99;
  background-color: #ffffff;
  display: flex;
  justify-content: space-around;
  align-items: center;

  .trues,
  .quick {
    box-sizing: border-box;
    width: 225rpx;
    height: 68rpx;
    line-height: 66rpx;
    font-size: 28rpx;
    letter-spacing: 3rpx;
    border-radius: 34rpx;
    text-align: center;
  }

  .trues {
    border: 1rpx solid #1d74fb;
    color: #1d74fb;
    &:active {
      border: 1rpx solid #024cbf;
      color: #024cbf;
    }
  }

  .quick {
    background-color: #1d74fb;
    color: #ffffff;
    &:active {
      background-color: #024cbf;
    }
  }
}

.slot-right {
  color: #1d74fb;
  font-size: 20rpx;
}

.popup-style {
  position: relative;
  width: 100%;
  height: auto;
  max-height: 1116rpx;
  min-height: 500rpx;
  border-radius: 10rpx;
  overflow-y: scroll;

  .top {
    position: sticky;
    top: 0;
    background: #ffffff;
    z-index: 99;
    .title {
      height: 100rpx;
      line-height: 100rpx;
      text-align: center;
      color: #444444;
      font-size: 28rpx;
    }

    .icon-close {
      position: absolute;
      display: block;
      width: 100rpx;
      height: 100rpx;
      top: 0rpx;
      right: 0rpx;
      line-height: 100rpx;
      display: flex;
      justify-content: center;
      align-items: center;

      .u-icon {
      }
    }
  }

  .subject-lists {
    position: relative;
    .item {
      box-sizing: border-box;
      padding: 0 36rpx;
      position: relative;
      width: 100%;
      height: 100rpx;
      line-height: 100rpx;
      display: flex;
      justify-content: space-between;
      &:active {
        background: #d9d8d8;
      }
      .name {
        font-size: 28rpx;
        color: #444444;
      }

      .score {
        font-size: 20rpx;
        color: #999999;
      }
    }
  }

  .random-btn-wrap {
    position: sticky;
    bottom: 0;
    width: 100%;
    height: auto;
    padding-bottom: 20rpx;
    z-index: 99;
    background-color: #ffffff;
    .random-btn {
      position: relative;
      width: 630rpx;
      margin: 0 auto;
      height: 80rpx;
      line-height: 80rpx;
      border-radius: 40rpx;
      text-align: center;
      color: #ffffff;
      background-color: #1d74fb;
      &:active {
        color: #ffffff;
        background: #024cbf;
      }
    }
  }
}
</style>
