<template>
	<view class="body">

		<!-- 操作菜单 -->
		<!-- 增加mask，全屏，让用户点击屏幕其它地方，都会隐藏菜单项 -->
		<view class="paper-left-popup-mask" v-show="show" @tap="hidepopup"></view>
		<view class="paper-left-popup" v-show="show">
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="addfriend">
				<view class="icon iconfont icon-sousuo"></view> 加糗友
			</view>
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="clear">
				<view class="icon iconfont icon-qingchu"></view> 清除缓存
			</view>
		</view>

		<!-- 小纸条列表 -->
		<block v-for="(item, index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>

		<!-- 上拉加载 -->
		<load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>
	// 小纸条组件
	import paperList from '../../components/paper/paper-list.vue';
	// 下拉加载更多
	import loadMore from "../../components/common/load-more.vue";

	export default {
		components: {
			paperList,
			loadMore,
		},
		data() {
			return {
				show: false,
				loadtext: "上拉加载更多",
				list: [{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称1",
						time: "10:21",
						data: "我是信息1",
						noreadnum: 2,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称2",
						time: "10:21",
						data: "我是信息2",
						noreadnum: 0,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称3",
						time: "10:21",
						data: "我是信息3",
						noreadnum: 0,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称4",
						time: "10:21",
						data: "我是信息4",
						noreadnum: 11,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称5",
						time: "10:21",
						data: "我是信息4",
						noreadnum: 11,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称6",
						time: "10:21",
						data: "我是信息4",
						noreadnum: 11,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称7",
						time: "10:21",
						data: "我是信息4",
						noreadnum: 11,
					},
					{
						userpic: "../../static/demo/userpic/12.jpg",
						username: "昵称8",
						time: "10:21",
						data: "我是信息4",
						noreadnum: 11,
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
		// 监听导航按钮点击事件
		onNavigationBarButtonTap(e) {
			// console.log(JSON.stringify(e));
			switch (e.index) {
				case 0:
					console.log("点击了左边按钮");
					this.hidepopup();
					break;
				case 1:
					console.log("点击了右边按钮");
					this.showpopup();
					break;
				default:
					break;
			}
		},
		methods: {
			// 操作菜单
			addfriend() {
				console.log("加糗友");
				this.hidepopup();
			},
			clear() {
				console.log("清除缓存");
				this.hidepopup();
			},
			hidepopup() {
				this.show = false;
			},
			showpopup() {
				this.show = true;
			},
			// 下拉刷新，获取数据
			getdata() {
				setTimeout(() => {
					// 服务器获取数据（模拟数据）
					let arr = [{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称5",
							time: "10:21",
							data: "我是信息5",
							noreadnum: 11,
						},
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称6",
							time: "10:21",
							data: "我是信息6",
							noreadnum: 11,
						},
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称7",
							time: "10:21",
							data: "我是信息7",
							noreadnum: 11,
						},
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "昵称8",
							time: "10:21",
							data: "我是信息8",
							noreadnum: 11,
						},
					];

					// 赋值
					this.list = arr;

					// 关闭下拉刷新，模拟2秒之后下拉刷新结束
					uni.stopPullDownRefresh();
				}, 2000);
			},
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
						username: "昵称-more",
						time: "10:21",
						data: "我是信息-more",
						noreadnum: 11,
					};
					this.list.push(obj);
					this.loadtext = "上拉加载更多";
				}, 1000);

				// this.loadtext = "没有更多数据了";
			},
		}
	}
</script>

<style>
	.body {
		padding: 0 20rpx;
	}

	.paper-left-popup-mask {
		position: fixed;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		/* background: #333; */
		z-index: 1999;
	}

	.paper-left-popup {
		position: fixed;
		right: 0;
		top: 10rpx;
		background: #FFF;
		z-index: 2000;
		width: 55%;
		box-shadow: 1rpx 1rpx 20rpx 2rpx #CCC;
	}

	.paper-left-popup>view {
		padding: 20rpx;
		font-size: 35rpx;
	}

	.paper-left-popup>view>view {
		margin-right: 10rpx;
		font-weight: bold;
	}

	.paper-left-popup-h {
		background: #EEE;
	}
</style>
