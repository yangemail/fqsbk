<template>
	<view>
		<!-- 聊天列表 -->
		<block v-for="(item, index) in list" :key="index">
			<!-- 时间 -->
			<view v-if="item.gstime" class="user-chat-time u-f-ajc">{{item.gstime}}</view>
			<!-- 使用u-f，因为不需要垂直方向居中 -->
			<view class="user-chat-list u-f" :class="{'user-chat-me':(item.isme)}">
				<!-- 好友的头像 -->
				<image v-if="!item.isme" :src="item.userpic" mode="widthFix" lazy-load></image>
				<view class="user-chat-list-body">
					<!-- 文字 -->
					<text v-if="item.type == 'text'">{{item.data}}</text>
					<!-- 图片 -->
					<image v-if="item.type == 'img'" :src="item.data" mode="widthFix" lazy-load></image>
				</view>
				<!-- 自己的头像 -->
				<image v-if="item.isme" :src="item.userpic" mode="widthFix" lazy-load></image>
			</view>
		</block>

		<!-- 聊天页面底部输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>

	</view>
</template>

<script>
	// 底部输入框
	import userChatBottom from "../../components/user-chat/user-chat-bottom.vue"
	// 时间功用函数
	import time from "../../common/time.js"

	export default {
		components: {
			userChatBottom
		},
		data() {
			return {
				list: []
			}
		},
		onLoad() {
			// let s1 = "1554970014";
			// let s2 = "1555146414";
			// let s3 = (new Date()).getTime();
			// console.log(time.gettime.gettime(s1));
			// console.log(time.gettime.gettime(s2));
			// console.log(time.gettime.gettime(s3));
			// 从服务器获取数据，一定要在onLoad(){}中，调用一下
			this.getData();
		},
		methods: {
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
			}
		}
	}
</script>

<style>
	.user-chat-time {
		padding: 50rpx 0;
		color: #A2A2A2;
		font-size: 24rpx;
	}

	.user-chat-list {
		padding: 20rpx 0;
	}

	.user-chat-list>image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		flex-shrink: 0;
	}

	.user-chat-list-body {
		position: relative;
		background: #F4F4F4;
		padding: 25rpx;
		margin-left: 20rpx;
		/* 防止数据过长触碰到右边 */
		margin-right: 100rpx;
		border-radius: 20rpx;
	}

	/* :after 选择器在被选元素的内容后面插入内容。请使用 content 属性来指定要插入的内容。*/
	.user-chat-list-body::after {
		position: absolute;
		left: -30rpx;
		right: 0;
		top: 30rpx;
		content: '';
		/* 需要加入width:0，否则从前到后的长度 */
		width: 0;
		height: 0;
		border: 16rpx solid #F4F4F4;
		/* 因为上面的border大小为16rpx，此处border-color为四部分组成。上、右、下、左 */
		border-color: transparent #F4F4F4 transparent transparent;
	}

	/* .user-chat-me是我自己发送的信息样式 */
	.user-chat-me {
		justify-content: flex-end;
	}

	/* 表示：.user-chat-me下面的.user-chat-list-body */
	.user-chat-me .user-chat-list-body {
		margin-right: 20rpx;
		margin-left: 100rpx;
	}

	.user-chat-me .user-chat-list-body::after {
		/* 默认值。通过浏览器计算左边缘的位置。 */
		left: auto;
		right: -30rpx;
		border-color: transparent transparent transparent #F4F4F4;
	}

	.user-chat-list-body>image {
		max-width: 150rpx;
		max-height: 200rpx;
	}
</style>
