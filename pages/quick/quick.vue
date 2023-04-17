<template>
  <view>
    <u-navbar :title="title" :safeAreaInsetTop="false">
      <view @click="onBack" class="u-nav-slot" slot="left">
        <u-icon name="arrow-left" size="19"></u-icon>
      </view>

      <view @click="open" class="u-nav-slot slot-right" slot="right">
        更换试卷
      </view>
    </u-navbar>
    <view class="quick-container"> 拼音 </view>

    <!-- <u-modal
      :show="show"
      @confirm="confirm"
      @cancel="OnExit"
      ref="uModal"
      :showCancelButton="true"
      confirmText="继续测试"
      cancelText="退出"
    >
      <view class="slot-content">
        <view class="text-center">确认现在退出考试？</view>
        <view>若选择继续测试将重考本题</view>
      </view>
    </u-modal> -->

    <u-popup :show="show" @close="close" @open="open" round="10">
      <view class="popup-style">
        <view class="top">
          <view class="title"> 选择试题 </view>
          <view class="icon-close" @click="close">
            <u-icon name="close" color="#1d74fb"></u-icon>
          </view>
        </view>
        <view class="subject-lists">
          <view
            class="item"
            @click="setSubject(i)"
            v-for="i in subjectLists"
            :key="i.name"
          >
            <view class="name">{{ i.name }}</view>
            <view class="score">{{ i.status ? i.score : "未测试" }}</view>
          </view>
        </view>
      </view>
    </u-popup>
  </view>
</template>

<script>
export default {
  data() {
    return {
      title: "真题模拟1",
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
    };
  },
  methods: {
    open() {
      this.show = true;
    },

    setSubject(item) {
      this.title = item.name;
      this.close();
    },
    close() {
      this.show = false;
    },
    onBack() {
      uni.navigateBack({
        animationType: "pop-out",
        animationDuration: 300,
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
.quick-container {
  margin-top: 64px;
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
}

// .text-center {
//   text-align: center;
// }
</style>