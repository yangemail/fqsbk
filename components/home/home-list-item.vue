<template>
	<!-- 功能列表 -->
	<view class="home-list-item u-f-ac u-f-jsb" hover-class="home-list-hover">
		<view class="u-f-ac">
			<view class="icon iconfont" :class="('icon-'+item.icon)"></view>{{item.name}}
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		data() {
			return {

			};
		}
	}
</script>

<style scoped>
	.home-list-hover {
		background-color: #F4F4F4;
	}

	.home-list-item {
		padding: 20rpx;
		border-top: 1rpx solid #F4F4F4;
		border-bottom: 1rpx solid #F4F4F4;
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
