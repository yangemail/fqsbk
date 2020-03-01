<template>
	<view>
		<!-- 背景图+用户基本信息 -->
		<user-space-head :userinfo="userinfo"></user-space-head>
		<!-- 统计 -->
		<view class="user-space-data">
			<home-data :homedata="spacedata"></home-data>
		</view>
		<!-- 统计和tab导航之间的分割线 -->
		<view style="height: 20rpx; background: #F4F4F4;"></view>
		<!-- tab导航 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap" scrollStyle="border-bottom:0;"
		 scrollItemStyle="width:33.33%;"></swiper-tab-head>

	</view>
</template>

<script>
	// 背景图+用户基本信息
	import userSpaceHead from "../../components/user-space/user-space-head.vue";
	// 统计数据组件
	import homeData from "../../components/home/home-data.vue";
	// Tab导航切换
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";

	export default {
		components: {
			userSpaceHead,
			homeData,
			swiperTabHead,
		},
		data() {
			return {
				tabIndex: 0,
				tabBars: [{
						name: "主页",
						id: "zhuye"
					},
					{
						name: "糗事",
						id: "qiushi"
					},
					{
						name: "动态",
						id: "dongtai"
					},
				],
				userinfo: {
					bgimg: 1,
					userpic: '../../static/demo/userpic/11.jpg',
					username: '昵称',
					sex: 0,
					age: 20,
					isguanzhu: false,
				},
				spacedata: [{
						name: "获赞",
						num: "10k"
					},
					{
						name: "关注",
						num: 11
					},
					{
						name: "粉丝",
						num: 12
					}
				],
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
	/* 公共间距 */
	.user-space-margin {
		margin: 15rpx 0;
	}

	.user-space-data {
		background: #FFFFFF;
		position: relative;
		z-index: 10;
		/* 左上角圆角 */
		border-top-left-radius: 20rpx;
		/* 右上角圆角 */
		border-top-right-radius: 20rpx;
		margin-top: -15rpx;
	}
</style>
