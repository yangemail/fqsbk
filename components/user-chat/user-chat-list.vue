<template>
	<!-- 聊天列表 -->
	<view class="user-chat-item">
		<!-- 时间 -->
		<view v-if="item.gstime" class="user-chat-time u-f-ajc">{{item.gstime}}</view>
		<!-- 使用u-f，因为不需要垂直方向居中 -->
		<view class="user-chat-list u-f" :class="{'user-chat-me':(item.isme)}">
			<!-- 好友的头像（左边） -->
			<image v-if="!item.isme" :src="item.userpic" mode="widthFix" lazy-load></image>
			<!-- 中间信息（文字、图片等） -->
			<view class="user-chat-list-body">
				<!-- 文字 -->
				<text v-if="item.type == 'text'">{{item.data}}</text>
				<!-- 图片 -->
				<image v-if="item.type == 'img'" :src="item.data" mode="widthFix" lazy-load></image>
			</view>
			<!-- 自己的头像（右边） -->
			<image v-if="item.isme" :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		data() {
			return {

			};
		}
	}
</script>

<style scoped>
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
	/* 设置justify-content: flex-end; 将所有信息放到最右边 */
	.user-chat-me {
		justify-content: flex-end;
	}

	/* 表示：.user-chat-me下面的.user-chat-list-body */
	/* 将消息体放到右边 */
	.user-chat-me .user-chat-list-body {
		margin-right: 20rpx;
		margin-left: 100rpx;
	}

	/* 设置消息体右边的小三角 */
	.user-chat-me .user-chat-list-body::after {
		/* 默认值。通过浏览器计算左边缘的位置。 */
		left: auto;
		right: -30rpx;
		border-color: transparent transparent transparent #F4F4F4;
	}

	/* 设置消息体中的图片最大宽度和高度 */
	.user-chat-list-body>image {
		max-width: 150rpx;
		max-height: 200rpx;
	}
</style>
