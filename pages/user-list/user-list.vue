<template>
	<!-- 好友列表页面 -->
	<view class="body">
		<!-- Tab 切换 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap" scrollStyle="border-bottom:0;"
		 scrollItemStyle="width:33%;"></swiper-tab-head>

		<!-- 好友列表 -->
		<view class="user-list u-f-ac">
			<!-- 左边：头像 -->
			<image src="../../static/demo/userpic/12.jpg" mode="widthFix" lazy-load></image>
			<!-- 中间：-->
			<view>
				<view>昵称</view>
				<view style="display: inline-block;">
					<tag-sex-age age="20" sex="0"></tag-sex-age>
				</view>
			</view>
			<!-- 右边：图标 -->
			<view class="icon iconfont icon-xuanze-yixuan u-f-ajc"></view>
		</view>

	</view>
</template>

<script>
	// 横向滚动组件
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	import tagSexAge from "../../components/common/tag-sex-age.vue";

	export default {
		components: {
			swiperTabHead,
			tagSexAge,
		},
		data() {
			return {
				tabIndex: 0,
				tabBars: [{
						name: "互关",
						id: "huguan",
						num: 10,
					},
					{
						name: "关注",
						id: "guanzhu",
						num: 20,
					},
					{
						name: "粉丝",
						id: "fensi",
						num: 30,
					},
				],
			}
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e) {
			// console.log(JSON.stringify(e));
			switch (e.index) {
				case 0:
					uni.navigateBack({
						delta: 1
					});
					break;
				default:
					break;
			}
		},
		methods: {
			// tabbar点击事件
			tabtap(index) {
				this.tabIndex = index;
			},
		}
	}
</script>

<style>
	.body {
		padding: 0 20rpx;
	}

	.user-list {
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEE;
	}

	.user-list>image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		margin-right: 20rpx;
		flex-shrink: 0;
	}

	.user-list>view:first-of-type {
		flex: 1;
		/* background: #007AFF; */
	}
	
	.user-list>view:first-of-type>view:first-child {
		font-size: 35rpx;
	}

	.user-list>view:last-of-type {
		width: 80rpx;
		/* background: yellow; */
		color: #CCC;
	}
	
</style>
