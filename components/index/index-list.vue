<template>
	<view class="index-list animated fadeInLeft fast">
		<view class="index-list1 u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<image :src="item.userpic" mode="widthFix" lazy-load></image>{{item.username}}
			</view>
			<view class="u-f-ac" v-show="!isguanzhu" @tap="guanzhu">
				<view class="icon iconfont icon-zengjia"></view>关注
			</view>
		</view>

		<view class="index-list2" @tap="opendetail">{{item.title}}</view>

		<view class="index-list3 u-f-ajc" @tap="opendetail">
			<!-- 图片部分 -->
			<image :src="item.titlepic" mode="widthFix" lazy-load></image>

			<!-- 视频部分 -->
			<template v-if="item.type == 'video'">
				<!-- 视频播放按钮 -->
				<view class="index-list-play icon iconfont icon-bofang"></view>
				<!-- 视频信息 -->
				<view class="index-list-playinfo">
					{{item.playnum}}次播放 {{item.long}}
				</view>
			</template>
		</view>

		<view class="index-list4 u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<view class="u-f-ac" :class="{'active':(infonum.index == 1)}" @tap="caozuo('ding')">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view>
					{{infonum.dingnum}}
				</view>
				<view class="u-f-ac" :class="{'active':(infonum.index == 2)}" @tap="caozuo('cai')">
					<view class="icon iconfont icon-kulian"></view>
					{{infonum.cainum}}
				</view>
			</view>
			<view class="u-f-ac">
				<view class="u-f-ac">
					<view class="icon iconfont icon-pinglun1"></view>
					{{item.commentnum}}
				</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa"></view>
					{{item.sharenum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script scoped>
	export default {
		props: {
			item: Object, // 传进来的对象
			index: Number, // 当前迭代索引，以后会经常用到
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu,
				infonum: this.item.infonum,
			};
		},
		methods: {
			// 关注事件
			guanzhu() {
				this.isguanzhu = true;
				uni.showToast({
					title: "关注成功",
				});
			},
			// 顶踩事件
			caozuo(type) {
				switch (type) {
					case "ding":
						if (this.infonum.index == 1) return;

						this.infonum.dingnum++;
						if (this.infonum.index == 2) {
							this.infonum.cainum--;
						}
						this.infonum.index = 1;
						break;
					case "cai":
						if (this.infonum.index == 2) return;

						this.infonum.cainum++;
						if (this.infonum.index == 1) {
							this.infonum.dingnum--;
						}
						this.infonum.index = 2;
						break;
					default:
						break;
				}
			},
			// 进入详情页
			opendetail() {
				console.log("点击进入内容详情页");
				uni.navigateTo({
					url: '../../pages/detail/detail?detailData='+JSON.stringify(this.item),
				});
			},
		},
	}
</script>

<style>
	.index-list {
		padding: 20rpx;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.index-list1>view:first-child {
		color: grey;
	}

	.index-list1>view:first-child>image {
		width: 85rpx;
		height: 85rpx;
		border-radius: 100%;
		margin-right: 10rpx;
	}

	.index-list1>view:last-child {
		background: #EEEEEE;
		border-radius: 5rpx;
		padding: 0 10rpx;
	}

	.index-list2 {
		padding-top: 15rpx;
		font-size: 32rpx;
	}

	.index-list3 {
		/* position:relative
		生成相对定位的元素，相对于其正常位置进行定位。
		因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。*/
		position: relative;
		padding-top: 15rpx;
	}

	.index-list3>image {
		width: 100%;
		border-radius: 20px;
	}

	.index-list-play {
		/* position: absolute
		 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
		 元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。*/
		position: absolute;
		font-size: 140rpx;
		color: white;
	}

	.index-list-playinfo {
		position: absolute;
		background: rgba(51, 51, 51, 0.72);
		color: white;
		bottom: 8rpx;
		right: 8rpx;
		border-radius: 40rpx;
		font-size: 22rpx;
		padding: 0 12upx;
	}

	.index-list4 {
		padding: 15rpx 0;
	}

	.index-list4 view {
		color: #B2B2B2;
	}

	.index-list4>view>view:first-child,
	.index-list4>view>view>view {
		margin-right: 10rpx;
	}

	.index-list4 .active,
	.index-list4 .active>view {
		color: #C5F61C;
	}
</style>
