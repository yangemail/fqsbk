<template>
	<view>

		<!-- 模糊背景+话题信息 -->
		<topic-info :item="topicInfo"></topic-info>

		<!-- 滚动tab导航开发：默认，最新 -->
		<!-- Tab 切换 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap" scrollStyle="border-bottom:0;"
		 scrollItemStyle="width:50%;"></swiper-tab-head>

		<!-- 列表 -->
		<view class="topic-detail-list">
			<block v-for="(item, index) in tablist" :key="index">
				<!-- 使用template，判断当前显示哪一个。没有选中的默认隐藏起来 -->
				<template v-if="tabIndex == index">
					<!-- 列表 -->
					<block v-for="(list, listindex) in item.list" :key="listindex">
						<common-list :item="list" :index="listindex"></common-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadtext="item.loadtext"></load-more>
				</template>
			</block>

		</view>

	</view>
</template>

<script>
	// 模糊背景，话题信息
	import topicInfo from "../../components/topic/topic-info.vue"
	// 横向滚动组件
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	// 关注中的动态列表组件
	import commonList from "../../components/common/common-list.vue";
	// 下拉加载更多
	import loadMore from "../../components/common/load-more.vue";

	export default {
		components: {
			topicInfo,
			swiperTabHead,
			commonList,
			loadMore,
		},
		data() {
			return {
				topicInfo: {
					titlepic: "../../static/demo/topicpic/13.jpeg",
					title: "忆往事，敬余生",
					desc: "我是描述",
					totalnum: "1000",
					todaynum: "800",
				},
				tabIndex: 0,
				tabBars: [{
						name: "默认",
						id: "moren"
					},
					{
						name: "最新",
						id: "zuixin"
					},
				],
				// tablist与tabBars是一一对应的
				tablist: [
					// 默认
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
					// 最新
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
		// 监听下拉刷新
		onPullDownRefresh() {
			this.getdata();
		},
		methods: {
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
			// 下拉刷新
			getdata() {
				setTimeout(()=>{
					// 获取数据（模拟数据）
					let arr = [
								// 文字例子
								{
									userpic: "../../static/demo/userpic/12.jpg",
									username: "文字例子，下拉刷新测试数据",
									sex: 1, //0:男，1:女
									age: 5,
									isguanzhu: false,
									title: "我是文字例子标题111",
									titlepic: "",
									video: false,
									share: false,
									path: "深圳 龙岗1111",
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
							];
					
					// 赋值
					this.tablist[this.tabIndex].list = arr;
					
					// 关闭下拉刷新，模拟2秒之后下拉刷新结束
					uni.stopPullDownRefresh();
				}, 2000);
			}
		}
	}
</script>

<style>

</style>
