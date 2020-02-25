<template>
	<!-- 好友列表页面 -->
	<view class="body">
		<!-- Tab 切换 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap" scrollStyle="border-bottom:0;"
		 scrollItemStyle="width:33%;"></swiper-tab-head>

		<!-- 好友列表 -->
		<!-- <block v-for="(item, index) in list" :key="index">
			<user-list :item="item" :index="index"></user-list>
		</block> -->
		<!-- 长列表横向滚动容器<swiper/> -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
				<swiper-item v-for="(items, index) in newsList" :key="index">
					<!-- <swiper-item > -->
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadmore(index)">
						<template v-if="items.list.length > 0">
							<!-- 图文列表组件 -->
							<block v-for="(item2, index2) in items.list" :key="index2">
								<!-- <index-list :item="item2" :index="index2"></index-list> -->
								<user-list :item="item2" :index="index2"></user-list>
							</block>

							<!-- 上拉加载 -->
							<load-more :loadtext="items.loadtext"></load-more>
						</template>

						<template v-else>
							<!-- 无内容，默认图片 -->
							<no-thing></no-thing>
						</template>

					</scroll-view>
				</swiper-item>
			</swiper>
		</view>

	</view>
</template>

<script>
	// 横向滚动组件
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	// 用户列表组件
	import userList from "../../components/user-list/user-list.vue";
	// 上拉加载更多
	import loadMore from "../../components/common/load-more.vue";
	// 默认空页面
	import noThing from "../../components/common/no-thing.vue";

	export default {
		components: {
			swiperTabHead,
			userList,
			loadMore,
			noThing
		},
		data() {
			return {
				swiperheight: 700,
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
				newsList: [{
						loadtext: "上拉加载更多",
						list: [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							age: 20,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称2",
							age: 21,
							sex: 1,
							isguanzhu: false
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称3",
							age: 23,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称4",
							age: 24,
							sex: 0,
							isguanzhu: true
						},{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							age: 20,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称2",
							age: 21,
							sex: 1,
							isguanzhu: false
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称3",
							age: 23,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称4",
							age: 24,
							sex: 0,
							isguanzhu: true
						}]
					},
					{
						loadtext: "上拉加载更多",
						list: [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							age: 20,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称2",
							age: 21,
							sex: 1,
							isguanzhu: false
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称3",
							age: 23,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称4",
							age: 24,
							sex: 0,
							isguanzhu: true
						}]
					},
					{
						loadtext: "上拉加载更多",
						list: [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							age: 20,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称2",
							age: 21,
							sex: 1,
							isguanzhu: false
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称3",
							age: 23,
							sex: 0,
							isguanzhu: true
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称4",
							age: 24,
							sex: 0,
							isguanzhu: true
						}]
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
		// 自动计算页面高度
		onLoad() {
			// onReady() {
			uni.getSystemInfo({
				success: (res) => {
					// 必须使用px，因为windowHeight返回的是px，不是rpx/upx
					let height = res.windowHeight - uni.upx2px(100);
					this.swiperheight = height;
				}
			})
		},
		methods: {
			// tabbar点击事件
			tabtap(index) {
				this.tabIndex = index;
			},
			// 滑动事件
			tabChange(e) {
				this.tabIndex = e.detail.current;
			},
			//上拉加载
			loadmore(index) {
				// 如果是：上拉加载更多，则不执行任何操作.
				if (this.newsList[index].loadtext !== "上拉加载更多") {
					return;
				}
				// 修改状态
				this.newsList[index].loadtext = "加载中...";
				// 获取数据
				setTimeout(() => {
					// 获取完成（假设这是服务端获取的数据，然后再将获取的数据追加到数组中）
					let obj = {
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称999",
						age: 999,
						sex: 1,
						isguanzhu: false
					};
					this.newsList[index].list.push(obj);
					this.newsList[index].loadtext = "上拉加载更多";
				}, 1000);

				// this.newsList[index].loadtext = "没有更多数据了";
			},
		}
	}
</script>

<style>
	/* .body {
		padding: 0 20rpx;
	} */
</style>
