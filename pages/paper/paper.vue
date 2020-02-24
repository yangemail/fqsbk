<template>
	<view class="body">
		<!-- 小纸条列表 -->
		<view class="paper-list u-f-ac">
			<!-- 左边：图标 -->
			<image src="../../static/demo/userpic/12.jpg" mode="widthFix" lazy-load></image>
			<!-- 右边： 两行 -->
			<view>
				<view class="u-f-ac u-f-jsb">昵称<view class="u-f-ajfe">10:21</view></view>
				<view class="u-f-ac u-f-jsb">我是信息
					<uni-badge class="uni-badge-left-margin" text="123" type="error" />
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '@/components/uni-badge/uni-badge.vue';

	export default {
		components: {
			uniBadge,
		},
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style>
	.body {
		padding: 0 20rpx;
	}

	.paper-list {
		border-bottom: 1rpx solid #EEE;
		padding: 20rpx 0;
	}

	.paper-list image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		margin-right: 20rpx;
		/* flex-shrink:0 表示不收右边挤压 */
		flex-shrink: 0;
	}

	.paper-list view {
		/* flex:1 表示右边填充剩余的空间 */
		flex: 1;
	}
	
	.paper-list>view>view:first-child {
		font-size: 35rpx;
		/* border: 1rpx solid; */
	}
	
	.paper-list>view>view:first-child>view{
		color: #CBCBCB;
		/* border: 1rpx solid red; */
	}
	
	.paper-list>view>view:last-child {
		color: #999;
	}
</style>
