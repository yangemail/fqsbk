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

		<!-- Tab切换页 -->
		<block v-for="(item, index) in tablist" :key="index">
			<!-- 主页 -->
			<template v-if="tabIndex == 0 && index == tabIndex">
				<user-space-userinfo :userinfo="userinfo"></user-space-userinfo>
			</template>
			<!-- 使用template，判断当前显示哪一个。没有选中的默认隐藏起来 -->
			<template v-else-if="tabIndex == index">
				<!-- 列表 -->
				<block v-for="(list, listindex) in item.list" :key="listindex">
					<common-list :item="list" :index="listindex"></common-list>
				</block>
				<!-- 上拉加载 -->
				<load-more :loadtext="item.loadtext"></load-more>
			</template>
		</block>
		
		<!-- 操作菜单 -->
		<user-space-popup :show="show" @hide="toggleShow" @lahei="lahei" @beizhu="beizhu"></user-space-popup>

	</view>
</template>

<script>
	// 背景图+用户基本信息
	import userSpaceHead from "../../components/user-space/user-space-head.vue";
	// 统计数据组件
	import homeData from "../../components/home/home-data.vue";
	// Tab导航切换
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	// 个人主页组件
	import userSpaceUserinfo from "../../components/user-space/user-space-userinfo.vue";
	// 动态列表组件
	import commonList from "../../components/common/common-list.vue";
	// 上拉加载更多
	import loadMore from "../../components/common/load-more.vue";
	// 右边Menu弹出菜单
	import userSpacePopup from "../../components/user-space/user-space-popup.vue";

	export default {
		components: {
			userSpaceHead,
			homeData,
			swiperTabHead,
			userSpaceUserinfo,
			commonList,
			loadMore,
			userSpacePopup,
		},
		data() {
			return {
				show: false,
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
					regtime: "2019-04-11",
					id: 1213,
					birthday: "1987-02-07",
					job: "IT",
					path: "广东广州",
					qg: "已婚"
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
				// tablist与tabBars是一一对应的
				tablist: [
					// 主页
					{ /*对象占位*/ },
					// 糗事
					{
						loadtext: "上拉加载更多",
						list: [ // 文字例子
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "文字例子",
								sex: 1, //0:男，1:女
								age: 25,
								isguanzhu: false,
								title: "我是文字例子标题",
								titlepic: "",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20,
							},
							// 图文例子
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "图文例子",
								sex: 0, //0:男，1:女
								age: 25,
								isguanzhu: false,
								title: "我是图文例子标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20,
							},
							// 视频例子
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "视频例子",
								sex: 0, //0:男，1:女
								age: 25,
								isguanzhu: false,
								title: "我是视频例子标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: {
									looknum: "20w",
									long: "2:47"
								},
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20,
							},
						]
					},
					// 粉丝
					{
						loadtext: "上拉加载更多",
						list: [
							// 文字例子
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "文字例子",
								sex: 1, //0:男，1:女
								age: 5,
								isguanzhu: false,
								title: "我是文字例子标题",
								titlepic: "",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20,
							},
							// 图文例子
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "图文例子",
								sex: 0, //0:男，1:女
								age: 2,
								isguanzhu: false,
								title: "我是图文例子标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20,
							},
							// 视频例子
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "视频例子",
								sex: 0, //0:男，1:女
								age: 6,
								isguanzhu: false,
								title: "我是视频例子标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: {
									looknum: "20w",
									long: "2:47"
								},
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20,
							},
						]
					},
				]
			}
		},
		// 上拉加载，上拉触底事件
		onReachBottom() {
			this.loadmore();
		},
		onNavigationBarButtonTap(e) {
			if(e.index == 0) {
				this.toggleShow();
			}
		},
		methods: {
			// 操作菜单显示隐藏
			toggleShow(){
				this.show = !this.show;
			},
			// 拉黑
			lahei() {
				console.log('拉黑');
				this.toggleShow();
			},
			// 备注
			beizhu() {
				console.log('备注')
				this.toggleShow();
			},
			// tabbar点击事件
			tabtap(index) {
				this.tabIndex = index;
			},
			// 上拉加载
			loadmore() {
				// 如果是：上拉加载更多，则不执行任何操作.
				if (this.tablist[this.tabIndex].loadtext !== "上拉加载更多") {
					return;
				}
				// 修改状态
				this.tablist[this.tabIndex].loadtext = "加载中...";
				// 获取数据
				setTimeout(() => {
					// 获取完成（假设这是服务端获取的数据，然后再将获取的数据追加到数组中）
					let obj = {
						userpic: "../../static/demo/userpic/12.jpg",
						username: "图文例子",
						sex: 0, //0:男，1:女
						age: 2,
						isguanzhu: false,
						title: "我是图文例子标题",
						titlepic: "../../static/demo/datapic/13.jpg",
						video: false,
						share: false,
						path: "深圳 龙岗",
						sharenum: 20,
						commentnum: 30,
						goodnum: 20,
					};
					this.tablist[this.tabIndex].list.push(obj);
					this.tablist[this.tabIndex].loadtext = "上拉加载更多";
				}, 1000);
				// this.tablist[this.tabIndex].loadtext = "没有更多数据了";
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
