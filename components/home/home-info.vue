<template>
		<!-- 登录 -->
		<view class="home-info u-f-ac" @tap="toUserSpace">
			<image :src="homeinfo.userpic" mode="widthFix" lazy-load></image>
			<view class="u-f1">
				<view>{{homeinfo.username}}</view>
				<view>总访客 {{homeinfo.totalnum}} 今日 {{homeinfo.todaynum}}</view>
			</view>
			<view class="icon iconfont icon-jinru"></view>
		</view>
</template>

<script>
	export default {
		props: {
			homeinfo: Object,
		},
		data() {
			return {
				
			};
		},
		methods: {
			toUserSpace() {
				uni.navigateTo({
					url: '../../pages/user-space/user-space',
				});
			}
		},
	}
</script>

<style scoped>
	.home-info {
		padding: 20rpx 40rpx;
	}

	.home-info>image {
		flex-shrink: 0;
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		margin-right: 15rpx;
	}

	/* 昵称 */
	.home-info>view:first-of-type>view:first-child {
		font-size: 32rpx;
	}

	/* 今日访客 */
	.home-info>view:first-of-type>view:last-child {
		color: #BBB;
	}

	.home-info>view:last-of-type {
		height: 100%;
	}
</style>
