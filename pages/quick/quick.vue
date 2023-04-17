<template>

	<view>
		<u-navbar :title="title" :safeAreaInsetTop="false">
			<view @click="onCancel" class="u-nav-slot" slot="left">
				<u-icon name="close" size="19"></u-icon>
			</view>
		</u-navbar>
		<view class="quick-container">
			拼音
		</view>

		<u-modal :show="show" @confirm="confirm" @cancel="OnExit" ref="uModal" :showCancelButton="true" confirmText="继续测试" cancelText="退出">
			<view class="slot-content">
				<view class="text-center">确认现在退出考试？</view>
				<view>若选择继续测试将重考本题</view>
			</view>
		</u-modal>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: "读多音节试题",
				show: false
			};
		},
		methods: {
			onCancel() {
				this.show = true;
			},
			confirm() {
				this.show = false;
			},
			OnExit() {
				this.show = false;
			}
		}
	}
</script>

<style lang="scss">
	.quick-container {
		margin-top: 64px;
		
	}
	.text-center{
		text-align: center;
	}
</style>