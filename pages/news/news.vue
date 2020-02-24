<template>
	<view>

		<!-- 自定义导航栏，:fixed=true固定导航栏 -->
		<news-nav-bar :tabBars="tabBars" :tabIndex="tabIndex" @change-tab="changeTab"></news-nav-bar>

		<!-- 列表 -->
		<!-- 长列表横向滚动容器<swiper/> -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
				<!-- 关注Tab页 -->
				<swiper-item>
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadmore()">
						<block v-for="(item, index) in guanzhu.list" :key="index">
							<!-- 动态列表组件 -->
							<common-list :item="item" :index="index"></common-list>
						</block>

						<!-- 上拉加载 -->
						<load-more :loadtext="guanzhu.loadtext"></load-more>
					</scroll-view>
				</swiper-item>
				
				<!-- 话题Tab页 -->
				<swiper-item>
					<scroll-view scroll-y="true" class="list">
						<!-- 话题：搜索框 -->
						<view class="search-input">
							<input class="uni-input " placeholder-class="topic-search icon iconfont icon-sousuo" placeholder="搜索内容" />
						</view>
						<!-- 话题：轮播图 : :indicator-dots：显示面板指示点（面板的三个点） :autoplay:自动播放 :interval:间隔播放多少秒 :duration:动画的过渡时间 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="(item, index) in topic.swiper" :key="index">
								<swiper-item>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 话题：热门分类（组件） -->
						<topic-nav :nav="topic.nav"></topic-nav>
						<!-- 话题：最近更新 -->
						<view class="topic-new">
							<view>最近更新</view>
							<block v-for="(item, index) in topic.list" :key="index">
								<topic-list :item="item" :index="index"></topic-list>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>

	</view>
</template>

<script>
	// 关注、话题uni-nav-bar组件
	import newsNavBar from "../../components/news/news-nav-bar.vue";
	// 关注中的动态列表组件
	import commonList from "../../components/common/common-list.vue";
	// 下拉加载更多
	import loadMore from "../../components/common/load-more.vue";
	// 热门分类
	import topicNav from "../../components/news/topic-nav.vue";
	// 最近更新列表
	import topicList from "../../components/news/topic-list.vue";

	export default {
		components: {
			newsNavBar,
			commonList,
			loadMore,
			topicNav,
			topicList,
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
						name: "话题",
						id: "topic"
					},
				],
				guanzhu: {
					loadtext: "上拉加载更多",
					list: [
						// 文字例子
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
						// 分享例子
						{
							userpic: "../../static/demo/userpic/12.jpg",
							username: "分享例子",
							sex: 0, //0:男，1:女
							age: 25,
							isguanzhu: false,
							title: "我是分享例子标题",
							titlepic: "",
							video: false,
							share: {
								title: "我是分享例子标题",
								titlepic: "../../static/demo/datapic/14.jpg"
							},
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 30,
							goodnum: 20,
						},
					]
				},
				// 轮播图
				topic: {
					swiper: [{
							src: "../../static/demo/banner2.jpg"
						},
						{
							src: "../../static/demo/banner2.jpg"
						},
						{
							src: "../../static/demo/banner2.jpg"
						},
					],
					nav: [{
							name: "最新"
						},
						{
							name: "游戏"
						},
						{
							name: "情感"
						},
						{
							name: "打卡"
						},
						{
							name: "故事"
						},
						{
							name: "喜爱"
						},
					],
					list: [{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10,
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10,
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10,
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10,
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10,
						},
						{
							titlepic: "../../static/demo/topicpic/13.jpeg",
							title: "话题名称",
							desc: "我是话题描述",
							totalnum: 50,
							todaynum: 10,
						}
					],
				}
			}
		},
		// 自动计算页面高度（展示高度）
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					// 必须使用px，因为windowHeight返回的是px，不是rpx/upx
					let height = res.windowHeight - uni.upx2px(100);
					this.swiperheight = height;
				}
			})
		},
		methods: {
			// 点击切换
			changeTab(index) {
				console.log("index from child component: " + index);
				this.tabIndex = index;
			},
			// 滑动事件
			tabChange(e) {
				this.tabIndex = e.detail.current;
			},
			// 上拉加载
			loadmore() {
				// 如果是：上拉加载更多，则不执行任何操作.
				if (this.guanzhu.loadtext !== "上拉加载更多") {
					return;
				}
				// 修改状态
				this.guanzhu.loadtext = "加载中...";
				// 获取数据
				setTimeout(() => {
					// 获取完成（假设这是服务端获取的数据，然后再将获取的数据追加到数组中）
					let obj = {
						userpic: "../../static/demo/userpic/12.jpg",
						username: "分享例子",
						sex: 0, //0:男，1:女
						age: 25,
						isguanzhu: false,
						title: "我是分享例子标题",
						titlepic: "",
						video: false,
						share: {
							title: "我是分享例子标题",
							titlepic: "../../static/demo/datapic/14.jpg"
						},
						path: "深圳 龙岗",
						sharenum: 20,
						commentnum: 30,
						goodnum: 20,
					};
					this.guanzhu.list.push(obj);
					this.guanzhu.loadtext = "上拉加载更多";
				}, 1000);

				// this.guanzhu.loadtext = "没有更多数据了";
			},
		}
	}
</script>

<style>
	.search-input {
		/* border: 1rpx solid red; */
		padding: 20rpx;
	}

	.search-input>input {
		/* border: 1rpx solid blue; */
		background: #F4F4F4;
		border-radius: 10rpx;
	}

	.topic-search {
		display: flex;
		justify-content: center;
		font-size: 27rpx;
	}

	.topic-swiper {
		padding: 0 20upx 20upx 20upx;
	}

	.topic-swiper image {
		width: 100%;
		border-radius: 10rpx;
	}

	/* 最近更新 */
	.topic-new {
		padding: 20rpx;
	}

	.topic-new>view:first-child {
		padding-bottom: 5rpx;
		font-size: 32rpx;
	}
</style>
