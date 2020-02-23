<template>
	<!-- 话题：热门分类 -->
	<view class="topic-nav">
		<!-- 第一行 -->
		<view class="u-f-ac u-f-jsb">
			<view>热门分类</view>
			<view class="u-f-ac" @tap="openTopicNav">
				更多<view class="icon iconfont icon-jinru"></view>
			</view>
		</view>
		<!-- 第二行 -->
		<view class="u-f-ac">
			<block v-for="(item, index) in nav" :key="index">
				<view class="u-f-ajc">{{item.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			nav: Array,
		},
		data() {
			return {

			};
		},
		methods: {
			openTopicNav() {
				uni.navigateTo({
					url: "../../pages/topic-nav/topic-nav"
				})
			}
		},
	}
</script>

<style scoped>
	.topic-nav {
		border-top: 1rpx solid #EEE;
		border-bottom: 1rpx solid #EEE;
		padding: 20rpx;
	}

	.topic-nav>view:first-child {
		margin-bottom: 10rpx;
	}

	.topic-nav>view:first-child view {
		color: #9e9e9e;
	}

	.topic-nav>view:first-child>view:first-child {
		color: #333;
		font-size: 32rpx;
	}

	.topic-nav>view:last-child {}

	.topic-nav>view:last-child>view {
		/* 每个flex元素平均分配 */
		flex: 1;
		background: #DDD;
		color: #9E9E9E;
		border-radius: 10rpx;
		margin: 0 10rpx;
	}
</style>
