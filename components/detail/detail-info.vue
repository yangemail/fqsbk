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
			<view>
				<!-- 第1行 -->
				<view class="u-f-ac u-f-jsb">
					<view class="u-f-ac">{{item.username}}
						<!-- 性别和年龄 -->
						<tag-sex-age :sex="item.sex" :age="item.age"></tag-sex-age>
					</view>
					<view v-show="!isguanzhu" class="icon iconfont icon-zengjia" @tap="guanzhu">关注</view>
				</view>
				<!-- 新增：增加昵称下面的时间，例如：26天前 -->
				<view class="common-list-right-time">26天前</view>
			</view>
			<!-- 第2行 -->
			<view>{{item.title}}</view>
			<!-- 第3行 -->
			<view class="u-f-ajc" style="flex-direction: column; height: auto;">
				<!-- 图片 -->
				<block v-for="(pic, index) in item.morepic" :key="index">
					<image :src="pic" mode="widthFix" lazy-load style="margin-bottom: 20rpx;" @tap="imgdetail(index)"></image>	
				</block>
				<!-- 视频 -->
				<!-- TODO: 讲解API接口的时候再具体讲解视频展示问题 -->
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
	import tagSexAge from "../common/tag-sex-age.vue";

	export default {
		components: {
			tagSexAge,
		},
		props: {
			item: Object
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
					title: "关注成功",
				});
			},
			// 点击的时候可以查看图片的大图
			imgdetail(index) {
				// 使用uni.previewImage(OBJECT)预览图片
				uni.previewImage({
					current: index,
					urls: this.item.morepic
				})
			}
		},
	}
</script>

<style scoped>
	@import url("../../common/list.css");

	/* 开始修改最下面的线，贯穿左和右侧 */
	.common-list-right {
		border-bottom: 0;
	}

	.common-list {
		border-bottom: 1rpx solid #EEE;
	}

	.common-list-right-time {
		padding: 15rpx 0;
		color: #CCC !important;
		font-size: 25rpx;
		background: #FFF !important;
	}

	.common-list-right>view:nth-child(1)>view:nth-child(1)>view:first-child {
		color: #999;
		font-size: 32rpx;
	}

	.common-list-right>view:nth-child(1)>view:nth-child(1)>view:last-child {
		background: #EEE;
		padding: 0 10rpx;
		font-size: 26rpx;
	}
</style>
