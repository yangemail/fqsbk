<template>
	<view class="topic-list u-f animated fadeInLeft fast" @tap="opendetail">
		<!-- 左边 -->
		<image :src="item.titlepic" mode="widthFix" lazy-load></image>
		<!-- 右边 -->
		<view>
			<view>#{{item.title}}#</view>
			<view>{{item.desc}}</view>
			<view>动态 {{item.totalnum}} 今日 {{item.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number,
		},
		data() {
			return {
				
			};
		},
		methods: {
			opendetail() {
				uni.navigateTo({
					url:"../../pages/topic-detail/topic-detail"
				})
			}
		},
	}
</script>

<style scoped>
.topic-list {
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEE;
	}

	.topic-list image {
		width: 150rpx;
		height: 150rpx;
		border-radius: 10rpx;
		margin-right: 20rpx;
	}

	.topic-list>view>view {
		color: #A4A4A4;
	}

	.topic-list>view>view:first-child {
		color: #333;
		font-size: 32rpx;
	}
</style>
