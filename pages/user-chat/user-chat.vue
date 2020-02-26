<template>
	<view>
		<!-- 聊天列表 -->
		<scroll-view id="scrollview" scroll-y :scroll-top="scrollTop" :scroll-with-animation="true" :style="{height: style.contentHeight+'px'}">
			<block v-for="(item, index) in list" :key="index">
				<user-chat-list :item="item" :index="index"></user-chat-list>
			</block>
		</scroll-view>

		<!-- 聊天页面底部输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>

	</view>
</template>

<script>
	// 时间公用函数
	import time from "../../common/time.js";
	// 用户聊天列表
	import userChatList from "../../components/user-chat/user-chat-list.vue";
	// 底部输入框
	import userChatBottom from "../../components/user-chat/user-chat-bottom.vue";

	export default {
		components: {
			userChatList,
			userChatBottom
		},
		data() {
			return {
				scrollTop: 0,
				style: {
					contentHeight: 0,
					itemHeight: 0
				},
				list: []
			}
		},
		onLoad() {
			// 从服务器获取数据，一定要在onLoad(){}中，调用一下
			this.getData();
			// 调用计算屏幕高度
			this.initdata();
		},
		onReady() {
			// 获取scrollTop位置信息
			this.pageToBottom();
		},
		methods: {
			// 初始化参数
			initdata() {
				try {
					const res = uni.getSystemInfoSync();
					// res.windowHeight：返回屏幕高度px。此时减去下面的输入条，获得<scroll-view/>需要的高度
					this.style.contentHeight = res.windowHeight - uni.upx2px(120);
				} catch (e) {
					//TODO handle the exception
				}
			},
			pageToBottom() {
				let q = uni.createSelectorQuery();
				q.select('#scrollview').boundingClientRect(); // 这个有什么用呢？
				q.selectAll('.user-chat-time').boundingClientRect();

				q.exec((res) => {
					// console.log("res: " + JSON.stringify(res));
					res[1].forEach((val) => {
						this.style.itemHeight += val.height;
					});

					// TODO: 还是有问题，长列表中不能自动显示最后一个消息。
					if (this.style.itemHeight > this.style.contentHeight) {
						this.scrollTop = this.style.itemHeight;
						// console.log("this.scrollTop: " + this.scrollTop)
					}
				});
			},
			// 聊天数据
			getData() {
				// 模拟：从服务器获取到的数据
				let arr = [{
						isme: false,
						userpic: "../../static/demo/userpic/11.jpg",
						type: "text",
						data: "哈哈哈",
						time: "1554970014",
						gstime: "" // 转化之后的时间格式，例如：12:00
					},
					{
						isme: true,
						userpic: "../../static/demo/userpic/10.jpg",
						type: "img",
						data: "../../static/demo/3.jpg",
						time: "1555146414",
						gstime: ""
					}
				];
				for (let i = 0; i < arr.length; i++) {
					// getChatTime，信息时间小于300秒（5分钟），则不重复显示时间
					arr[i].gstime = time.gettime.getChatTime(arr[i].time, i > 0 ? arr[i - 1].time : 0);
				}
				this.list = arr;
			},
			// 发送留言逻辑
			submit(data) {
				console.log("当前输入的是：" + data);
				
				// 构建数据
				let now = new Date().getTime();
				let obj = {
					isme: true, // 发送输入框，肯定是自己发送的，所以为true
					userpic: "../../static/demo/userpic/10.jpg",
					type: "text",
					data: data,
					time: now,
					gstime: time.gettime.getChatTime(now, this.list[this.list.length - 1].time)
				};

				this.list.push(obj);

				// 每次提交之后，重新计算底部滚动条位置
				this.pageToBottom();
			}
		}
	}
</script>

<style>

</style>
