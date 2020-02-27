<template>
	<!-- 第三方登录 -->
	<view class="other-login u-f-ac">
		<view class="u-f-ajc u-f1">
			<view class="icon iconfont icon-weixin u-f-ajc"></view>
		</view>
		<view class="u-f-ajc u-f1">
			<view class="icon iconfont icon-xinlangweibo u-f-ajc"></view>
		</view>
		<view class="u-f-ajc u-f1">
			<view class="icon iconfont icon-QQ u-f-ajc"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		}
	}
</script>

<style scoped>
	.other-login {
		padding: 20rpx 80rpx;
	}

	.other-login>view>view {
		width: 100rpx;
		height: 100rpx;
		/* border: 1rpx solid; */
		border-radius: 100%;
		font-size: 55rpx;
		color: #FFF;
	}

	.other-login .icon-QQ {
		background-color: #2CAEFC;
	}

	.other-login .icon-weixin {
		background-color: #2BD19B;
	}

	.other-login .icon-xinlangweibo {
		background-color: #FC7729;
	}
</style>
