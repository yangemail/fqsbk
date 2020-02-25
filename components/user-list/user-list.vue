<template>
	
	<!-- 好友列表 -->
	<view class="user-list u-f-ac animated fadeInLeft fast">
		<!-- 左边：头像 -->
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<!-- 中间：-->
		<view>
			<view>{{item.username}}</view>
			<view style="display: inline-block;">
				<tag-sex-age :age="item.age" :sex="item.sex"></tag-sex-age>
			</view>
		</view>
		<!-- 右边：图标 -->
		<view class="icon iconfont u-f-ajc" :class="(item.isguanzhu) ? 'icon-xuanze-yixuan' : 'icon-zengjia1'"></view>
	</view>
	
</template>

<script>
	// 性别和年龄组件
	import tagSexAge from "../../components/common/tag-sex-age.vue";

	export default {
		components: {
			tagSexAge,
		},
		props: {
			item: {
				type: Object,
				default: null,
			},
			index: {
				type: Number,
				default: 0,
			}
		},
		data() {
			return {

			};
		}
	}
</script>

<style scoped>
	.user-list {
		margin: 0 20rpx;
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEE;
	}

	.user-list>image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		margin-right: 20rpx;
		flex-shrink: 0;
	}

	.user-list>view:first-of-type {
		flex: 1;
		/* background: #007AFF; */
	}

	.user-list>view:first-of-type>view:first-child {
		font-size: 35rpx;
	}

	.user-list>view:last-of-type {
		width: 80rpx;
		/* background: yellow; */
		color: #CCC;
	}

	.icon-zengjia1 {
		color: #F8791B !important;
	}
</style>
