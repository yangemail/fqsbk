<template>
	<!-- 动态列表组件 -->
	<view class="common-list u-f animated fadeInLeft fast">
		<!-- 左侧头像 -->
		<view class="common-list-left">
			<image :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
		<!-- 右侧内容 -->
		<view class="common-list-right">
			<!-- 右边分为4行 -->
			<!-- 第1行 -->
			<view class="u-f-ac u-f-jsb">
				<view class="u-f-ac">{{item.username}}
					<!-- 性别和年龄 -->
					<view class="tag-sex icon iconfont " :class="[item.sex == 0 ? 'icon-nan' : 'icon-nv']">{{item.age}}</view>
				</view>
				<view v-show="!isguanzhu" class="icon iconfont icon-zengjia" @tap="guanzhu">关注</view>
			</view>
			<!-- 第2行 -->
			<view>{{item.title}}</view>
			<!-- 第3行 -->
			<view class="u-f-ajc">
				<!-- 图片 -->
				<image v-if="item.titlepic" :src="item.titlepic" mode="widthFix" lazy-load></image>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang"></view>
					<view class="common-list-playinfo">
						{{item.video.looknum}} 次播放 {{item.video.long}}
					</view>
				</template>
				<!-- 分享元素样式：左边-》图片，右边-》标题 -->
				<view class="common-list-share u-f-ac" v-if="item.share">
					<image :src="item.share.titlepic" mode="widthFix" lazy-load></image>
					<view>{{item.share.title}}</view>
				</view>
			</view>
			<!-- 第4行 -->
			<view class="u-f-ac u-f-jsb">
				<view>{{item.path}}</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa">{{item.sharenum}}</view>
					<view class="icon iconfont icon-pinglun1">{{item.commentnum}}</view>
					<view class="icon iconfont icon-dianzan1">{{item.goodnum}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: {
				type: Object,
			},
			index: {
				type: Number,
			},
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu
			};
		},
		methods: {
			guanzhu() {
				this.isguanzhu = true;
				uni.showToast({
					title:"关注成功",
				});
			},
		},
	}
</script>

<style scoped>
	/* 列表组件 */
	.common-list {
		padding: 20rpx;
	}

	.common-list-left {
		/* 防止flex布局被压缩 */
		flex-shrink: 0;

	}

	.common-list-left image {
		width: 90rpx;
		height: 90rpx;
		border-radius: 100%;
	}

	.common-list-right {
		/* 需要让元素自动填充满右面的空间 - flex:1 */
		flex: 1;
		margin-left: 15rpx;
		border-bottom: 1rpx solid #EEE;
		padding-bottom: 10rpx;
	}

	.common-list-right>view:nth-child(1)>view:first-child {
		color: #999;
		font-size: 32rpx;
	}

	.common-list-right>view:nth-child(1)>view:first-child .tag-sex {
		background: #007AFF;
		color: #FFF;
		font-size: 23rpx;
		padding: 5rpx 10rpx;
		margin-left: 10rpx;
		border-radius: 20rpx;
		line-height: 22rpx;
	}

	.common-list-right>view:nth-child(1)>view:last-child {
		background: #EEE;
		padding: 0 10rpx;
		font-size: 26rpx;
	}

	.common-list-right>view:nth-child(2) {
		font-size: 32rpx;
		padding: 12rpx 0;
	}

	.common-list-right>view:nth-child(3) {
		position: relative;
		margin-bottom: 10rpx;
	}

	.common-list-right>view:nth-child(3)>image {
		width: 100%;
		border-radius: 10rpx;
	}

	.common-list-play,
	.common-list-playinfo {
		position: absolute;
		color: #FFF;
	}

	.common-list-play {
		font-size: 130rpx;
	}

	.common-list-playinfo {
		right: 10rpx;
		bottom: 10rpx;
		background: rgba(51, 51, 51, 0.73);
		border-radius: 20rpx;
		padding: 0 20rpx;
		font-size: 26rpx;
	}

	.common-list-share {
		background: #EEE;
		/* border: 1rpx solid; */
		width: 100%;
		padding: 10rpx;
		border-radius: 10rpx;
	}

	.common-list-share>image {
		width: 200rpx;
		height: 150rpx;
		margin-right: 10rpx;
	}

	.common-list-right>view:nth-child(4) {}

	.common-list-right>view:nth-child(4)>view {
		color: #AAA;
	}

	.common-list-right>view:nth-child(4)>view:nth-child(2)>view {
		margin-left: 10rpx;
		padding-left: 5rpx;
		font-size: 28rpx;
	}
</style>
