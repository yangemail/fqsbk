<template>
	<view>

		<!-- 滚动tab导航开发 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap"></swiper-tab-head>

		<!-- 长列表横向滚动容器<swiper/> -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
				<swiper-item v-for="(items, index) in newsList" :key="index">
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadmore(index)">
						<template v-if="items.list.length > 0">
							<!-- 图文列表组件 --> 
							<block v-for="(item2, index2) in items.list" :key="index2">
								<index-list :item="item2" :index="index2"></index-list>
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
	// 引入组件
	import indexList from "../../components/index/index-list.vue";
	// 横向滚动组件
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	// 上拉加载更多
	import loadMore from "../../components/common/load-more.vue";
	// 默认空页面
	import noThing from "../../components/common/no-thing.vue";

	export default {
		components: {
			indexList,
			swiperTabHead,
			loadMore,
			noThing,
		},
		data() {
			return {
				swiperheight: 700,
				tabIndex: 0,
				tabBars: [{
						name: "关注",
						id: "guanzhu"
					},
					{
						name: "推荐",
						id: "tuijian"
					},
					{
						name: "体育",
						id: "tiyu"
					},
					{
						name: "热点",
						id: "redian"
					},
					{
						name: "财经",
						id: "caijing"
					},
					{
						name: "娱乐",
						id: "yule"
					},
				],
				newsList: [{
						loadtext: "上拉加载更多",
						list: [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 1, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}]
					},
					{
						loadtext: "上拉加载更多",
						list: [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 1, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 1, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}]
					},
					{
						loadtext: "上拉加载更多",
						list: [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 1, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 1, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: false,
							title: "我是标题",
							type: "img", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}, {
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称",
							isguanzhu: true,
							title: "我是标题",
							type: "video", // 图片或者视频类型,img:图文,video:视频
							titlepic: "../../static/demo/datapic/11.jpg",
							playnum: "20w",
							long: "2:47",
							infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
								index: 1, // 0：还没有操作；1：已经顶了；2：已经踩了
								dingnum: 11,
								cainum: 11,
							},
							commentnum: 10,
							sharenum: 10,
						}]
					},
					{
						loadtext: "上拉加载更多",
						list: []
					},
					{
						loadtext: "上拉加载更多",
						list: []
					},
					{
						loadtext: "上拉加载更多",
						list: []
					}
				],
			}
		},
		// 自动计算页面高度
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					// 必须使用px，因为windowHeight返回的是px，不是rpx/upx
					let height = res.windowHeight - uni.upx2px(100);
					this.swiperheight = height;
				}
			})
		},
		// 监听搜索框点击事件，跳转到search页面
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
				url: "../search/search"
			});
		},
		// 监听原生标题导航按钮点击事件，进入发布页面
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 1:
					//打开发布页面（笔图标）
					uni.navigateTo({
						url: "../add-input/add-input"
					})
					break;
				default:
					break;
			}
		},
		methods: {
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
						username: "昵称",
						isguanzhu: false,
						title: "我是标题",
						type: "img", // 图片或者视频类型,img:图文,video:视频
						titlepic: "../../static/demo/datapic/11.jpg",
						infonum: { // 顶和踩 -》（需要限制刷量，顶踩只能一次而且二选一）
							index: 0, // 0：还没有操作；1：已经顶了；2：已经踩了
							dingnum: 11,
							cainum: 11,
						},
						commentnum: 10,
						sharenum: 10,
					};
					this.newsList[index].list.push(obj);
					this.newsList[index].loadtext = "上拉加载更多";
				}, 1000);

				// this.newsList[index].loadtext = "没有更多数据了";
			},
			// tabbar点击事件
			tabtap(index) {
				this.tabIndex = index;
			},
			// 滑动事件
			tabChange(e) {
				this.tabIndex = e.detail.current;
			},
		}
	}
</script>

<style>

</style>
