<template>
	<view>
		<template v-if="!islogin">
			<!-- 未登录 -->
			<view class="u-f-ajc">登录仿糗事百科，体验更多功能</view>
			<!-- 第三方登录 -->
			<other-login></other-login>
			<!-- 账号密码登录 -->
			<view class="u-f-ajc" @tap="openLogin">账号密码登录<view class="icon iconfont icon-jinru"></view>
			</view>
		</template>

		<template v-else>
			<!-- 登录 -->
			<home-info :homeinfo="homeinfo"></home-info>
		</template>

		<!-- 糗事、动态、评论、收藏：数据 -->
		<home-data :homedata="homedata"></home-data>

		<!-- 广告位 -->
		<view class="home-adv u-f-ajc">
			<image src="../../static/demo/demo20.jpg" mode="widthFix" lazy-load></image>
		</view>

		<!-- 功能列表 -->
		<view class="home-list">
			<block v-for="(item, index) in list" :key="index">
				<home-list-item :item="item" :index="index"></home-list-item>
			</block>
		</view>
	</view>
</template>

<script>
	// 功能列表
	import homeListItem from "../../components/home/home-list-item.vue";
	// 登录信息
	import homeInfo from "../../components/home/home-info.vue";
	// 第三方登录
	import otherLogin from "../../components/home/other-login.vue";
	// 糗事、动态、评论、收藏：数据
	import homeData from "../../components/home/home-data.vue";

	export default {
		components: {
			homeListItem,
			homeInfo,
			otherLogin,
			homeData
		},
		data() {
			return {
				islogin: true,
				// 登录
				homeinfo: {
					userpic: "../../static/demo/userpic/11.jpg",
					username: "昵称",
					totalnum: 0,
					todaynum: 0
				},
				// 糗事、动态、评论、收藏：数据
				homedata: [{
						name: "糗事",
						num: 0
					},
					{
						name: "动态",
						num: 0
					},
					{
						name: "评论",
						num: 0
					},
					{
						name: "收藏",
						num: 0
					}
				],
				// 功能列表
				list: [{
					icon: "liulan",
					name: "浏览历史",
					clicktype: "",
					url: ""
				}, {
					icon: "huiyuanvip",
					name: "糗百认证",
					clicktype: "",
					url: ""
				}, {
					icon: "keyboard",
					name: "审核糗事",
					clicktype: "",
					url: ""
				}]
			}
		},
		onNavigationBarButtonTap(e) {
			console.log("Menu button is tapped (index): " + e.index);
			switch (e.index) {
				case 0:
					console.log("跳转到设置页面");
					uni.navigateTo({
						url: '../user-set/user-set',
					});
					break;
				default:
					break;
			}
		},
		methods: {
			openLogin() {
				uni.navigateTo({
					url: '../login/login',
				});
			}
		}
	}
</script>

<style>
	.home-adv {
		padding: 20rpx;
	}

	.home-adv>image {
		border-radius: 20rpx;
		/* 最好给一个告诉,否则进入页面的时候,图片会闪烁一下 */
		height: 150rpx;
	}

	.home-list {
		padding: 20rpx;
	}
</style>
