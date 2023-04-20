<template>
  <u-popup :show="show" round="10">
    <view class="popup-style">
      <view class="t1">确认现在退出考试?</view>
      <view class="t2">若选择退出将重考</view>
      <view class="btn-wrap">
        <view class="btn-sm-default" @click="back"> 退出 </view>
        <view class="btn-sm-primary" @click="close">继续测试</view>
      </view>
    </view>
  </u-popup>
</template>

<script>
export default {
  props: {
    show: {
      default: false,
      type: Boolean,
    },
  },
  data() {
    return {};
  },
  methods: {
    close() {
      this.$emit("close", false);
    },
    back() {
      this.close();
      uni.switchTab({
        url: "/pages/index/index",
      });
    },
  },
};
</script>

<style scoped lang="scss">
.popup-style {
  box-sizing: border-box;
  padding-top: 72rpx;
  position: relative;
  width: 100%;
  height: 400rpx;
  border-radius: 10rpx;
  display: flex;
  flex-direction: column;
  align-items: center;

  .t1 {
    color: #444444;
    font-size: 32rpx;
    height: 32rpx;
    line-height: 32rpx;
    margin-bottom: 40rpx;
  }

  .t2 {
    color: #999999;
    font-size: 28rpx;
    height: 28rpx;
    line-height: 28rpx;
    margin-bottom: 67rpx;
  }

  .btn-wrap {
    display: flex;
    /deep/ .btn-sm-default {
      margin-right: 72rpx;
    }
  }
}
</style>
