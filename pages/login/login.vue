<template>
  <view class="container">
    <image class="logo" src="../../static/logo.png"></image>

    <view class="form-wrap">
      <view class="form-item">
        <image class="icon" src="../../static/username@2x.png"></image>
		<!-- 注意：由于兼容性差异，如果需要使用前后插槽，nvue下需使用u--input，非nvue下需使用u-input -->
		<!-- #ifndef APP-NVUE -->
	<u-input
	     placeholder="请输入手机号码"
          border="bottom"
          type="number"
          maxlength="11">
	 <!-- #endif -->
	 <!-- #ifdef APP-NVUE -->
	<u--input
		 placeholder="请输入手机号码"
          border="bottom"
          type="number"
          maxlength="11">
	<!-- #endif -->
		<template slot="suffix">
		<u-code
			@end="end"
			@start="start"
			ref="uCode"
			@change="codeChange"
			:seconds="seconds"
			changeText="X秒重新获取">
		</u-code>
			<u-button
				@tap="getCode"
				:text="tips"
				type="default"
				size="mini"
				>

			</u-button>
		</template>
	<!-- #ifndef APP-NVUE -->
	</u-input>
	<!-- #endif -->
	<!-- #ifdef APP-NVUE -->
	</u--input>
	<!-- #endif -->
    </view>
      <view class="form-item">
        <image class="icon" src="../../static/passwd@2x.png"></image>
        <u--input placeholder="请输入验证码" border="bottom"></u--input>
      </view>
    </view>

    <view class="sigin-btn" @click="onSubmit">登录</view>
    <view class="login-btn">免费注册</view>

    <view class="file-wrap">
      <checkbox-group @change="onChange">
        <label>
          <checkbox class="custom-checkbox" value="cb" />
        </label>
      </checkbox-group>
      <text class="file-txt"
        >请阅读并同意
        <view class="navigator" @click="toPage('')">《用户协议》</view>和
        <view class="navigator" @click="toPage('')">《隐私协议》</view></text
      >
    </view>

    <u-toast ref="uToast"></u-toast>
  </view>
</template>

<script>
export default {
  data() {
    return {
      value: false,
      checked: false,
      tips: "发送验证码",
      seconds: 60,
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

    onChange(e) {
      console.log(e.detail.value.length);
      if (e.detail.value.length) {
        this.checked = true;
      } else {
        this.checked = false;
      }
    },

    onSubmit() {
      if (this.checked) {
      } else {
        // console.log(uni.$u);
        this.$refs.uToast.show({
          type: "default",
          title: "默认主题",
          message: "请勾选协议文件",
        });
      }
    },

    codeChange(text) {
      this.tips = text;
    },

    getCode() {
      if (this.$refs.uCode.canGetCode) {
        // 模拟向后端请求验证码
        uni.showLoading({
          title: "正在获取验证码",
        });
        setTimeout(() => {
          uni.hideLoading();
          // 这里此提示会被this.start()方法中的提示覆盖
          uni.$u.toast("验证码已发送");
          // 通知验证码组件内部开始倒计时
          this.$refs.uCode.start();
        }, 2000);
      } else {
        uni.$u.toast("倒计时结束后再发送");
      }
    },
  },
};
</script>

<style lang="scss">
.container {
  position: relative;
  width: 100%;
  box-sizing: border-box;
  padding: 146rpx 60rpx 0rpx;

  .logo {
    display: block;
    width: 220rpx;
    height: 220rpx;
    margin: 0 auto 174rpx auto;
  }

  .form-wrap {
    position: relative;
    margin-bottom: 72rpx;
    .form-item {
      position: relative;
      display: flex;
      align-items: center;
      &:first-child {
        margin-bottom: 25rpx;
      }
      .icon {
        display: block;
        width: 48rpx;
        height: 48rpx;
      }
    }
  }

  .sigin-btn {
    position: relative;
    width: 100%;
    height: 88rpx;
    line-height: 88rpx;
    text-align: center;
    background-color: #1d74fb;
    color: #ffffff;
    font-size: 32rpx;
    letter-spacing: 20rpx;
    border-radius: 44rpx;
    margin-bottom: 10rpx;
    &:active {
      background-color: #4388ef;
    }
  }

  .login-btn {
    position: relative;
    width: 300rpx;
    margin: 0 auto;
    height: 88rpx;
    line-height: 88rpx;
    text-align: center;
    background-color: transparent;
    color: #999999;
    font-size: 24rpx;
    letter-spacing: 4rpx;
    &:active {
      color: #4388ef;
    }
  }

  .file-wrap {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 150rpx;
    line-height: 150rpx;
    background: rgba(29, 116, 251, 0.1);
    border-top-right-radius: 20rpx;
    border-top-left-radius: 20rpx;
    display: flex;
    justify-content: center;
    align-items: center;

    .custom-checkbox {
      /deep/ .uni-checkbox-input {
        width: 24rpx;
        height: 24rpx;
        border-radius: 50%;
        border-width: 1rpx;
        &:hover {
          border-color: #979797;
        }
      }

      /deep/ .uni-checkbox-input-checked:before {
        content: "";
        font-size: 22px;
        position: absolute;
        width: 20rpx;
        height: 20rpx;
        border-radius: 50%;
        background: #979797;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        -webkit-transform: translate(-50%, -50%);
      }
    }
    .file-txt {
      font-size: 20rpx;
      color: #999999;
    }
    .navigator {
      display: inline-block;
      height: 22rpx;
      line-height: 20rpx;
      color: #4388ef;
      z-index: 99;
    }
  }
}
</style>
