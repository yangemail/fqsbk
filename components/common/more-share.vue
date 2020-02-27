<template>
	<view class="animated fadeIn faster" v-if="show">
		<!-- 分享更多功能 -->
		<!-- 这个view标签是蒙版 -->
		<view class="more-share-model"  @tap="toggle"></view>
		<!-- 这个view分为上中下三部分 -->
		<view class="more-share">
			<view class="more-share-title u-f-ajc">分享到</view>
			<scroll-view scroll-x class="more-share-body">
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-weixin u-f-ajc more-share-wx"></view>
					<view>微信</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-weixin u-f-ajc more-share-pyq"></view>
					<view>朋友圈</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-xinlangweibo u-f-ajc more-share-wb"></view>
					<view>新浪微博</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-QQ u-f-ajc more-share-qq"></view>
					<view>QQ好友</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-QQ u-f-ajc more-share-qq"></view>
					<view>其它</view>
				</view>
			</scroll-view>
			<view class="more-share-bottom u-f-ajc" hover-class="more-share-hover" @tap="toggle">取消</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			show: Boolean
		},
		data() {
			return {

			};
		},
		methods: {
			toggle() {
				this.$emit('toggle');
			}
		},
	}
</script>

<style scoped>
	/* 分享到功能 */
	
	/* 蒙版class */
	.more-share-model {
		background-color: rgba(51, 51, 51, 0.49);
		position: fixed;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		z-index: 100;
	}

	.more-share {
		position: fixed;
		z-index: 110;
		bottom: 0;
		left: 0;
		right: 0;
		background: #FFF;
	}

	.more-share-title,
	.more-share-bottom {
		font-size: 32rpx;
		padding: 25rpx;
	}

	.more-share-body {
		/* 规定段落中的文本不进行换行 */
		white-space: nowrap;
		width: 100%;
		height: 200rpx;
		border-bottom: 1rpx solid #EEE;
		display: flex !important;
		/* line-height 属性设置行间的距离（行高） */
		line-height: 200rpx !important;
	}

	.more-share-item {
		width: 25%;
		/* inline-flex：将对象作为“内联块级”弹性伸缩盒显示 VS. flex： 将对象作为弹性伸缩盒显示*/
		display: inline-flex;
		justify-content: center;
		align-items: center;
		/* column：纵向排列 */
		flex-direction: column;
		height: 100%;
	}

	.more-share-hover {
		background: #EEE;
	}

	.more-share-item>view:first-child {
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		/* border: 1rpx solid; */
		font-size: 55rpx;
		color: #FFF;
	}

	.more-share-item>view:last-child {
		color: #7A7A7A;
	}

	.more-share-wx {
		background: #15AD9F;
	}

	.more-share-pyq {
		background: #504E4C;
	}

	.more-share-wb {
		background-color: #EE5E5E;
	}

	.more-share-qq {
		background-color: #4A73BA;
	}
</style>
