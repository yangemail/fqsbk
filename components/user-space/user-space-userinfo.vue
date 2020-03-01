<template>
	<!-- 主页 -->
	<view class="user-space-userinfo">
		<view class="user-space-userinfo-item">
			<view class="">账号信息</view>
			<view class="">糗龄：{{getRegAge}}</view>
			<view class="">糗百ID：{{userinfo.id}}</view>
		</view>
		<view class="user-space-userinfo-item">
			<view class="">个人信息</view>
			<view class="">星座：{{getHoroscope}}</view>
			<view class="">职业：{{userinfo.job}}</view>
			<view class="">故乡：{{userinfo.path}}</view>
			<view class="">情感：{{userinfo.qg}}</view>
		</view>
	</view>
</template>

<script>
	// 公共事件函数库
	import time from "../../common/time.js";

	export default {
		props: {
			userinfo: Object,
		},
		computed: {
			getRegAge() {
				return time.gettime.sumAge(this.userinfo.regtime);
			},
			getHoroscope() {
				return time.gettime.getHoroscope(this.userinfo.birthday);
			}
		}
	}
</script>

<style scoped>
	.user-space-userinfo {
		padding: 0 30rpx;
	}

	.user-space-userinfo-item {
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.user-space-userinfo-item>view {
		color: #AAAAAA;
	}

	.user-space-userinfo-item>view:first-child {
		color: #333333;
		font-size: 35rpx;
		padding: 15rpx 0;
	}
</style>
