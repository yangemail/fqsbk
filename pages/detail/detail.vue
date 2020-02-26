<template>
	<view>
		<detail-info :item="detail"></detail-info>
	</view>
</template>

<script>
	import detailInfo from "../../components/detail/detail-info.vue"

	export default {
		components: {
			detailInfo
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
			}
		},
		onLoad(e) {
			console.log("--- onLoad(e) is called. ---")
			this.initdata(JSON.parse(e.detailData)); // 将首页传入的JSON字符串，转换为Object
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
			}
		}
	}
</script>

<style>

</style>
