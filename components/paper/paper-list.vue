<template>

	<!-- 小纸条列表 -->
	<view class="paper-list u-f-ac animated fadeIn fast"  @tap="opendetail">
		<!-- 左边：图标 -->
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<!-- 右边： 两行 -->
		<view>
			<view class="u-f-ac u-f-jsb">{{item.username}}
				<view class="u-f-ajfe">{{item.time}}</view>
			</view>
			<view class="u-f-ac u-f-jsb">{{item.data}}
				<template v-if="item.noreadnum>0">
					<uni-badge class="uni-badge-left-margin" :text="item.noreadnum" type="error" />
				</template>
			</view>
		</view>
	</view>

</template>

<script scoped>
	import uniBadge from '@/components/uni-badge/uni-badge.vue';

	export default {
		components: {
			uniBadge,
		},
		props: {
			item: {
				type: Object,
				default: null
			},
			index: {
				type: Number,
				default: 0
			}
		},
		data() {
			return {

			};
		},
		methods: {
			opendetail() {
				uni.navigateTo({
					url: '../../pages/user-chat/user-chat',
				});
			}
		},
	}
</script>

<style scoped>
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

	.paper-list>view>view:first-child>view {
		color: #CBCBCB;
		/* border: 1rpx solid red; */
	}

	.paper-list>view>view:last-child {
		color: #999;
	}
</style>
