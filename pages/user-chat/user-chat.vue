<template>
	<view>

		<!-- 聊天列表 -->
		<!-- 使用u-f，因为不需要垂直方向居中 -->
		<view class="user-chat-list u-f user-chat-me">
			<!-- 头像 -->
			<!-- <image src="../../static/demo/userpic/11.jpg" mode="widthFix" lazy-load></image> -->
			<view class="user-chat-list-body">
				<!-- 文字 -->
				<!-- <text>随便随便随便随便随便随便</text> -->
				<!-- 图片 -->
				<image src="../../static/demo/3.jpg" mode="widthFix" lazy-load></image>
			</view>
			<image src="../../static/demo/userpic/11.jpg" mode="widthFix" lazy-load></image>
		</view>

		<!-- 聊天页面底部输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>

	</view>
</template>

<script>
	import userChatBottom from "../../components/user-chat/user-chat-bottom.vue"

	export default {
		components: {
			userChatBottom
		},
		data() {
			return {

			}
		},
		methods: {
			// 发送留言逻辑
			submit(data) {
				console.log("当前输入的是：" + data);
			}
		}
	}
</script>

<style>
	.user-chat-list {}

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
	
	.user-chat-list-body >image {
		max-width: 150rpx;
		max-height: 200rpx;
	}
</style>
