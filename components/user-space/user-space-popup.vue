<template>
	<view>
		<!-- 增加mask，全屏，让用户点击屏幕其它地方，都会隐藏菜单项 -->
		<view class="paper-left-popup-mask" v-show="show" @tap="hidepopup"></view>
		<view class="paper-left-popup" v-show="show">
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="lahei">
				<view class="icon iconfont icon-sousuo"></view> 拉黑
			</view>
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="beizhu">
				<view class="icon iconfont icon-qingchu"></view> 备注
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			show: {
				type: Boolean,
				default: false
			},
		},
		data() {
			return {

			};
		},
		methods: {
			// 拉黑
			lahei() {
				console.log("拉黑");
				this.$emit("lahei");
			},
			// 备注
			beizhu() {
				console.log("备注");
				this.$emit("beizhu");
			},
			// 隐藏弹出菜单
			hidepopup() {
				this.$emit("hide");
			},
		},
	}
</script>

<style scoped>
	.paper-left-popup-mask {
		position: fixed;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		/* background: #333; */
		z-index: 1999;
	}

	.paper-left-popup {
		position: fixed;
		right: 0;
		top: 100rpx;
		background: #FFF;
		z-index: 2000;
		width: 55%;
		box-shadow: 1rpx 1rpx 20rpx 2rpx #CCC;
	}

	.paper-left-popup>view {
		padding: 20rpx;
		font-size: 35rpx;
	}

	.paper-left-popup>view>view {
		margin-right: 10rpx;
		font-weight: bold;
	}

	.paper-left-popup-h {
		background: #EEE;
	}
</style>
