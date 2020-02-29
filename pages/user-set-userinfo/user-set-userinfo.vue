<template>
	<view class="body">
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>头像</view>
			<view class="u-f-ac" @tap="changeimg">
				<image :src="userpic" mode="aspectFill" lazy-load></image>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>昵称</view>
			<view class="u-f-ac">
				<view>昵称</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>性别</view>
			<view class="u-f-ac">
				<view>不限</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>生日</view>
			<view class="u-f-ac">
				<view>2019-3-16</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>情感</view>
			<view class="u-f-ac">
				<view>已婚</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>职业</view>
			<view class="u-f-ac">
				<view>IT</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f-ac u-f-jsb">
			<view>家乡</view>
			<view class="u-f-ac">
				<view>中国广州</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<button type="primary" class="user-set-btn" @tap="submit">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 后期此头像需要从服务器进行获取（当前登录用户的头像）
				userpic:"../../static/demo/userpic/11.jpg",
				
			}
		},
		methods: {
			submit() {

			},
			// 用户修改头像
			changeimg() {
				uni.chooseImage({
					count:1,
					sizeType:['compressed'],
					success: (res) => {
						this.userpic = res.tempFilePaths[0];
					}
				})
			}
		}
	}
</script>

<style>
	/* css 引入需要放到第一行 */
	@import url("../../common/form.css");

	.user-set-userinfo-list {
		padding: 20rpx;
		border-bottom: 1rpx solid #F4F4F4;
	}

	.user-set-userinfo-list>view:first-child {
		font-size: 32rpx;
		font-weight: bold;
		color: #9B9B9B;
	}

	.user-set-userinfo-list>view:last-child>image {
		width: 80rpx;
		height: 80rpx;
		border-radius: 100%;

	}

	.user-set-userinfo-list>view:last-child>view:last-of-type {
		margin-left: 10rpx;
		color: #9B9B9B;
	}
</style>
