<template>
	<!-- 糗事、动态、评论、收藏：数据 -->
	<view class="home-data u-f-ac">
		<block v-for="(item, index) in homedata" :key="index">
			<view class="u-f1 u-f-ajc u-f-column">
				<view class="">{{item.num}}</view>{{item.name}}
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		props: {
			homedata: Array,
		},
		data() {
			return {

			};
		}
	}
</script>

<style scoped>

	.home-data {
		padding: 20rpx 40rpx;
	}

	.home-data>view {
		color: #989898;
	}

	.home-data>view>view {
		font-size: 32rpx;
		color: #333;
	}
</style>
