<template>
	<view>
		<template v-if="islogin">
			<!-- 未登录 -->
			<view class="u-f-ajc">登录仿糗事百科，体验更多功能</view>
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
			<!-- 账号密码登录 -->
			<view class="u-f-ajc">账号密码登录<view class="icon iconfont icon-jinru"></view>
			</view>
		</template>
		<!-- 登录 -->
		<view class="home-info u-f-ac">
			<image src="../../static/demo/userpic/11.jpg" mode="widthFix" lazy-load></image>
			<view class="u-f1">
				<view>昵称</view>
				<view>总访客 0 今日 0</view>
			</view>
			<view class="icon iconfont icon-jinru"></view>
		</view>

		<!-- 糗事、动态、评论、收藏：数据 -->
		<view class="home-data u-f-ac">
			<view class="u-f1 u-f-ajc u-f-column">
				<view class="">0</view>糗事
			</view>
			<view class="u-f1 u-f-ajc u-f-column">
				<view class="">0</view>动态
			</view>
			<view class="u-f1 u-f-ajc u-f-column">
				<view class="">0</view>评论
			</view>
			<view class="u-f1 u-f-ajc u-f-column">
				<view class="">0</view>收藏
			</view>
		</view>
		<!-- 广告位 -->
		<view class="home-adv u-f-ajc">
			<image src="../../static/demo/demo20.jpg" mode="widthFix" lazy-load></image>
		</view>
		<!-- 功能列表 -->
		<view class="home-list">
			<view class="home-list-item u-f-ac u-f-jsb" hover-class="home-list-hover">
				<view class="u-f-ac">
					<view class="icon iconfont icon-liulan"></view>浏览历史
				</view>
				<view class="icon iconfont icon-jinru"></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		components: {

		},
		data() {
			return {
				islogin: false,
			}
		},
		onNavigationBarButtonTap(e) {
			console.log("Menu button is tapped (index): " + e.index);
			switch (e.index) {
				case 0:
					console.log("跳转到设置页面");
					break;
				default:
					break;
			}
		},
		methods: {

		}
	}
</script>

<style>
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

	.home-data {
		padding: 20rpx 40rpx;
	}

	.home-data>view {
		color: #989898;
	}

	.home-data>view>view {
		font-size: 32rpx;
		color: #333;
	}

	.home-adv {
		padding: 20rpx;
	}

	.home-adv>image {
		border-radius: 20rpx;
		/* 最好给一个告诉,否则进入页面的时候,图片会闪烁一下 */
		height: 150rpx;
	}

	.home-list {
		padding: 20rpx;
	}

	.home-list-hover {
		background-color: #F4F4F4;
	}

	.home-list-item {
		padding: 20rpx;
		border-top: 1rpx solid #EEE;
		border-bottom: 1rpx solid #EEE;
	}

	.home-list-item>view:first-child {
		color: #333;
	}

	.home-list-item>view:first-child>view {
		margin-right: 10rpx;
	}

	.home-list-item>view:last-child {
		color: #CCC;
	}
</style>
