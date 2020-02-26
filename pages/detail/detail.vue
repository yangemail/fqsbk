<template>
	<view>

		<!-- 详情列表 -->
		<detail-info :item="detail"></detail-info>

		<!-- 评论列表 -->
		<view class="u-comment-title">最新评论 {{comment.count}}</view>
		<view class="uni-comment u-comment">
			<block v-for="(item, index) in comment.list" :key="index">
				<comment-list :item="item" :index="index"></comment-list>
			</block>
		</view>
	</view>
</template>

<script>
	// 详情列表
	import detailInfo from "../../components/detail/detail-info.vue";
	// 时间公用方法
	import time from "../../common/time.js";
	// 评论列表
	import commentList from "../../components/detail/comment-list.vue";

	export default {
		components: {
			detailInfo,
			commentList
		},
		data() {
			return {
				// 演示数据
				detail: {
					userpic: "../../static/demo/userpic/12.jpg",
					username: "图文例子",
					sex: 0, //0:男，1:女
					age: 25,
					isguanzhu: false,
					title: "我是图文例子标题",
					titlepic: "../../static/demo/datapic/13.jpg", // 默认选择第一个，从morepic[]中，默认选择第一个，放在titlepic里面，作为封面图
					morepic: ["../../static/demo/datapic/13.jpg", "../../static/demo/datapic/14.jpg",
						"../../static/demo/datapic/15.jpg"
					], // 数组的形式，因为上传多图的时候是一个数组，显示的时候默认显示第一张图片。所以后台上传和数据库对应的字段应该是morepic
					video: false,
					share: false,
					path: "深圳 龙岗",
					sharenum: 20,
					commentnum: 30,
					goodnum: 20,
				},
				comment: {
					count: 20, // 数据库中评论的总数，并不是本数组获取到的数量
					list: []
				}
			}
		},
		onLoad(e) {
			console.log("--- onLoad(e) is called. ---")

			// 获取前一个页面传入的JSON数据
			this.initdata(JSON.parse(e.detailData)); // 将首页传入的JSON字符串，转换为Object

			// 初始化数据
			this.getcomment();
		},
		// 监听导航右边按钮点击事件
		onNavigationBarButtonTap(e) {
			if (e.index == 0) {
				console.log("分享按钮点击了！");
			}
		},
		methods: {
			// 初始化数据
			initdata(obj) {
				// 修改窗口标题：uni.setNavigationBarTitle(OBJECT)：动态设置当前页面的标题。
				uni.setNavigationBarTitle({
					title: obj.title
				});
			},
			getcomment() {
				let arr = [
					// 一级评论
					{
						id: 1,
						fid: 0, // 父级评论ID，如果是1级评论，默认为0
						userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username: "小猫咪",
						time: "1555400035",
						data: "支持国产，支持DCloud!"
					},
					// 子级评论
					{
						id: 2,
						fid: 1, // 父级评论ID，如果是1级评论，默认为0
						userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username: "小猫咪",
						time: "1555400035",
						data: "支持国产，支持DCloud!"
					},
					// 子级评论
					{
						id: 3,
						fid: 1, // 父级评论ID，如果是1级评论，默认为0
						userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username: "小猫咪",
						time: "1555400035",
						data: "支持国产，支持DCloud!"
					},
					// 一级评论
					{
						id: 4,
						fid: 0, // 父级评论ID，如果是1级评论，默认为0
						userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
						username: "小猫咪",
						time: "1555400035",
						data: "支持国产，支持DCloud!"
					},
				];
				for (let i = 0; i < arr.length; i++) {
					arr[i].time = time.gettime.gettime(arr[i].time);
				}
				this.comment.list = arr;
			}
		}
	}
</script>

<style>
	.u-comment-title {
		padding: 20rpx;
		font-size: 30rpx;
		font-weight: bold;
	}

	.u-comment {
		padding: 0 20rpx;
	}
</style>
