<template>
  <view class="sound-icon">
    <view class="sound-wave">
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
      <view class="bar"></view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>

<style scoped lang="scss">
.sound-icon {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.sound-wave {
  width: 250rpx;
  height: 90rpx;
  display: flex;
  justify-content: space-around;
  align-items: center;

  .bar {
    display: block;
    width: 2rpx;
    margin-right: 2rpx;
    height: 90rpx;
    background: #ffffff;
    animation: sound 0ms -800ms linear infinite alternate;
    transition: height 0.8s;
  }
}

@keyframes sound {
  0% {
    opacity: 0.35;
    height: 7px;
  }
  100% {
    opacity: 1;
    height: 55rpx;
  }
}

.bar:nth-child(1) {
  height: 2px;
  animation-duration: 474ms;
}
.bar:nth-child(2) {
  height: 10px;
  animation-duration: 433ms;
}
.bar:nth-child(3) {
  height: 18px;
  animation-duration: 407ms;
}
.bar:nth-child(4) {
  height: 26px;
  animation-duration: 458ms;
}
.bar:nth-child(5) {
  height: 30px;
  animation-duration: 400ms;
}
.bar:nth-child(6) {
  height: 32px;
  animation-duration: 427ms;
}
.bar:nth-child(7) {
  height: 34px;
  animation-duration: 441ms;
}
.bar:nth-child(8) {
  height: 36px;
  animation-duration: 419ms;
}
.bar:nth-child(9) {
  height: 40px;
  animation-duration: 487ms;
}
.bar:nth-child(10) {
  height: 46px;
  animation-duration: 442ms;
}
.bar:nth-child(11) {
  height: 2px;
  animation-duration: 474ms;
}
.bar:nth-child(12) {
  height: 10px;
  animation-duration: 433ms;
}
.bar:nth-child(13) {
  height: 18px;
  animation-duration: 407ms;
}
.bar:nth-child(14) {
  height: 26px;
  animation-duration: 458ms;
}
.bar:nth-child(15) {
  height: 30px;
  animation-duration: 400ms;
}
.bar:nth-child(16) {
  height: 32px;
  animation-duration: 427ms;
}
.bar:nth-child(17) {
  height: 34px;
  animation-duration: 441ms;
}
.bar:nth-child(18) {
  height: 36px;
  animation-duration: 419ms;
}
.bar:nth-child(19) {
  height: 40px;
  animation-duration: 487ms;
}
.bar:nth-child(20) {
  height: 46px;
  animation-duration: 442ms;
}
</style>
