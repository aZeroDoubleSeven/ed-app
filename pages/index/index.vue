<template>
  <view class="container">
    <view class="top-wrap">
      <view class="title">普通话测验</view>
      <image class="icon-pu" src="../../static/index_top_bg_pu.png"></image>
    </view>

    <view class="score-wrap">
      <view class="level">预测等级:二级甲等</view>
      <view class="num-list">
        <view class="item">
          <view class="num">92</view>
          <view class="name">单音字</view>
        </view>
        <view class="item">
          <view class="num">92</view>
          <view class="name">多音字</view>
        </view>
        <view class="item">
          <view class="num">92</view>
          <view class="name">短文</view>
        </view>
        <view class="item">
          <view class="num">92</view>
          <view class="name">命题</view>
        </view>
      </view>
      <view class="btn-wrap">
        <view class="test-log">测试报告</view>
        <view class="test-quick">快速测试</view>
      </view>
    </view>

    <view class="other-pages">
      <view class="page">
        <image class="icons" src="../../static/icon_entry@2x.png"></image>
        <view class="name">报名入口</view>
      </view>
      <view class="page">
        <image class="icons" src="../../static/icon_query@2x.png"></image>
        <view class="name">分数查询</view>
      </view>
      <view class="page">
        <image class="icons" src="../../static/icon_scores@2x.png"></image>
        <view class="name">报名须知</view>
      </view>
      <view class="page">
        <image class="icons" src="../../static/icon_training@2x.png"></image>
        <view class="name">训练记录</view>
      </view>
    </view>

    <view class="training-wrap">
      <view class="normal-box">
        <view class="box-title">常规训练</view>
        <view class="train-lists">
          <view class="item words">单词练习</view>
          <view class="item expressions">词语练习</view>
          <view class="item article">短文练习</view>
          <view class="item article-title">命题练习</view>
        </view>
      </view>
      <view class="plus-box">
        <view class="box-title">强化训练</view>
        <view class="bad-words">
          <view class="title">常错别字词</view>
          <view class="nums">累积: 300</view>
        </view>
        <view class="collect-words">
          <view class="title">收藏字词</view>
          <view class="nums">累积: 1000</view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {},
};
</script>

<style lang="scss">
.container {
  position: relative;
  width: 100%;
  box-sizing: border-box;
  padding: 127rpx 28rpx 0rpx 28rpx;

  .top-wrap {
    position: absolute;
    top: 0;
    right: 0;
    box-sizing: border-box;
    padding-top: 50rpx;
    padding-left: 28rpx;
    width: 100%;
    height: 427rpx;
    background: #1d74fb;

    .title {
      font-size: 40rpx;
      font-family: SourceHanSansCN-Medium, SourceHanSansCN;
      font-weight: 500;
      color: #ffffff;
      line-height: 40rpx;
      letter-spacing: 4rpx;
    }

    .icon-pu {
      position: absolute;
      width: 250rpx;
      height: 200rpx;
      top: 60rpx;
      right: 40rpx;
      display: block;
    }
  }

  .score-wrap {
    position: relative;
    box-sizing: border-box;
    padding: 24rpx;
    margin: 0 auto 40rpx auto;
    width: 100%;
    height: 384rpx;
    background: #ffffff;
    box-shadow: 0rpx 2rpx 10rpx 1rpx rgba(0, 0, 0, 0.1);
    border-radius: 20rpx;

    .level {
      font-size: 32rpx;
      line-height: 32rpx;
      height: 32rpx;
      color: #444444;
      margin-bottom: 48rpx;
      letter-spacing: 4rpx;
    }

    .num-list {
      position: relative;
      display: flex;
      justify-content: space-around;
      margin-bottom: 64rpx;

      .item {
        width: 100rpx;

        .num {
          text-align: center;
          font-size: 32rpx;
          color: #999999;
          line-height: 32rpx;
          margin-bottom: 24rpx;
        }

        .name {
          text-align: center;
          font-size: 28rpx;
          color: #999999;
          line-height: 28rpx;
        }
      }
    }

    .btn-wrap {
      position: relative;
      display: flex;
      justify-content: center;
      .test-log {
        width: 252rpx;
        height: 68rpx;
        line-height: 68rpx;
        font-size: 28rpx;
        color: #1d74fb;
        border-radius: 34rpx;
        text-align: center;
        background: #ffffff;
        border: 1rpx solid #1d74fb;
        margin-right: 45rpx;

        &:active {
          color: #ffffff;
          background: #1d74fb;
        }
      }

      .test-quick {
        width: 252rpx;
        height: 68rpx;
        line-height: 68rpx;
        font-size: 28rpx;
        color: #ffffff;
        border-radius: 34rpx;
        text-align: center;
        background: #1d74fb;
        border: 1rpx solid #1d74fb;
        &:active {
          color: #ffffff;
          background: #024cbf;
        }
      }
    }
  }

  .other-pages {
    position: relative;
    display: flex;
    justify-content: space-around;
    width: 100%;
    height: auto;
    margin-bottom: 40rpx;
    .page {
      position: relative;
      display: flex;
      flex: 0 0 140rpx;
      height: 140rpx;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      &:active {
        background-color: #ffffff;
        box-shadow: 0rpx 2rpx 10rpx 1rpx rgba(0, 0, 0, 0.1);
      }
      .icons {
        display: block;
        width: 60rpx;
        height: 60rpx;
        margin-bottom: 20rpx;
      }

      .name {
        font-size: 24rpx;
        line-height: 24rpx;
        text-align: center;
        color: #444444;
      }
    }
  }

  .training-wrap {
    position: relative;
    display: flex;
    justify-content: space-between;

    .normal-box,
    .plus-box {
      position: relative;
      box-sizing: border-box;
      padding: 24rpx;
      width: 335rpx;
      height: 416rpx;
      background-color: #ffffff;
      border-radius: 30rpx;

      .box-title {
        line-height: 32rpx;
        font-size: 32rpx;
        height: 32rpx;
        color: #444444;
        margin-bottom: 32rpx;
        letter-spacing: 3.5rpx;
      }
    }

    .normal-box {
      .train-lists {
        position: relative;
        .item {
          box-sizing: border-box;
          padding-left: 24rpx;
          border-radius: 30rpx;
          width: 100%;
          height: 52rpx;
          line-height: 52rpx;
          font-size: 28rpx;
          color: #666666;
          letter-spacing: 4rpx;
          background-color: #edf3ff;
          margin-bottom: 24rpx;

          &:active {
            background-color: #d8e4fa;
          }
        }
      }
    }

    .plus-box {
      position: relative;
      .bad-words,
      .collect-words {
        position: relative;
        box-sizing: border-box;
        padding: 24rpx;
        width: 100%;
        height: 128rpx;
        border-radius: 20rpx;

        .title {
          color: #666666;
          font-size: 28rpx;
          height: 28rpx;
          line-height: 28rpx;
          letter-spacing: 4rpx;
          margin-bottom: 20rpx;
        }

        .nums {
          color: #999999;
          font-size: 20rpx;
          height: 20rpx;
          line-height: 20rpx;
          letter-spacing: 2rpx;
        }
      }

      .bad-words {
        background-color: #edf7ff;
        margin-bottom: 16rpx;
        &:active {
          background-color: #d8e4fa;
        }
      }

      .collect-words {
        background-color: #f0faf9;
        &:active {
          background-color: #cbeae7;
        }
      }
    }
  }
}
</style>
