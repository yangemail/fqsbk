<template>
	<view>
		<!-- 评论列表 -->
		<view class="uni-comment-list " :class="{'u-comment-list-child':(item.fid>0)}">
			<view class="uni-comment-face">
				<image :src="item.userpic" mode="widthFix"></image>
			</view>
			<view class="uni-comment-body">
				<view class="uni-comment-top">
					<text>{{item.username}}</text>
				</view>
				<view class="uni-comment-content">{{item.data}}</view>
				<view class="uni-comment-date">
					<view>{{item.time}}</view>
					<!-- <view class="uni-comment-replay-btn">5回复</view> -->
				</view>
			</view>
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
	.u-comment-list-child {
		padding: 20rpx;
		background: #F4F4F4;
		border-bottom: 1rpx solid #EEE;
		/* box-sizing 以特定的方式定义匹配某个区域的特定元素。
		通过将 box-sizing 设置为 "border-box"。这可令浏览器呈现出带有指定宽度和高度的框，并把边框和内边距放入框中。 */
		box-sizing: border-box;
		/* 将公共css中的外边距设为0 */
		margin: 0;
		/* 然后再更改margin-left为70rpx */
		margin-left: 70rpx;
		/* 确保元素不会超出范围 */
		width: auto;
	}
</style>
