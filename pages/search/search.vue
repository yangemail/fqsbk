<template>
	<view>
		<template v-if="list.length > 0">
			<!-- 图文列表组件 -->
			<block v-for="(item, index) in list" :key="index">
				<index-list :item="item" :index="index"></index-list>
			</block>

			<!-- 上拉加载 -->
			<load-more :loadtext="loadtext"></load-more>
			
		</template>

		<template v-else-if="issearch && list.length == 0">
			<!-- 无内容，默认图片 -->
			<no-thing></no-thing>
		</template>
	</view>
</template>

<script>
	// 引入组件
	import indexList from "../../components/index/index-list.vue";
	// 默认空页面
	import noThing from "../../components/common/no-thing.vue";
	// 上拉加载更多
	import loadMore from "../../components/common/load-more.vue";

	export default {
		components: {
			indexList,
			noThing,
			loadMore
		},
		data() {
			return {
				issearch: false,
				loadtext: "上拉加载更多",
				list: [],
			}
		},
		// 监听原生标题导航按钮点击事件
		onNavigationBarButtonTap(e) {
			// console.log(JSON.stringify(e))
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				});
			}
		},
		// 监听搜索框文本变化
		onNavigationBarSearchInputChanged(e) {
			console.log('监听搜索框文本变化: ' + e.text);
			// if (e.text) {
			// 	this.getdata(e.text);
			// }
		},
		// 监听点击搜索按钮事件(小键盘上面的“搜索”按钮)
		onNavigationBarSearchInputConfirmed(e) {
			console.log('监听点击搜索按钮事件: ' + e.text);
			if (e.text) {
				this.getdata(e.text);
			}
		},
		// 监听下拉刷新
		onPullDownRefresh() {
			// this.getdata();
			console.log("监听下拉刷新事件");
		},
		// 上拉加载，上拉触底事件。监听页面触底事件
		onReachBottom() {
			this.loadmore();
		},
		methods: {
			// 下拉刷新
			// getdata() {
			// 	setTimeout(() => {
			// 		// 获取数据（模拟数据）
			// 		let arr = [

			// 		];

			// 		// 赋值
			// 		// this.tablist[this.tabIndex].list = arr;

			// 		// 关闭下拉刷新，模拟2秒之后下拉刷新结束
			// 		uni.stopPullDownRefresh();
			// 	}, 2000);
			// },
			// 上拉加载
			loadmore() {
				// 如果是：上拉加载更多，则不执行任何操作.
				if (this.loadtext !== "上拉加载更多") {
					return;
				}
				// 修改状态
				this.loadtext = "加载中...";
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
					this.list.push(obj);
					this.loadtext = "上拉加载更多";
				}, 1000);

				// this.tablist[this.tabIndex].loadtext = "没有更多数据了";
			},
			// 搜索事件
			getdata(val) {
				// 显示加载提示框
				uni.showLoading({
					title: '加载中'
				});
				// 请求服务器：post请求，keyword=val
				setTimeout(() => {
					let arr = [{
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
					}];
					this.list = arr;

					// uni.showLoading(OBJECT) 显示 loading 提示框, 需主动调用 uni.hideLoading 才能关闭提示框。
					uni.hideLoading();
					
					this.issearch = true;
				}, 1000);
			}
		},
	}
</script>

<style>

</style>
