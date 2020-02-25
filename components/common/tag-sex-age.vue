<template>
		<!-- 性别和年龄 -->
		<view class="tag-sex icon iconfont " :class="[sex == 0 ? 'icon-nan' : 'icon-nv']">{{age}}</view>
</template>

<script>
	export default {
		props: {
			sex:Number,
			age:Number,
		},
		data() {
			return {
				
			};
		}
	}
</script>

<style scoped>
	.tag-sex {
		background: #007AFF;
		color: #FFF;
		font-size: 23rpx;
		padding: 5rpx 10rpx;
		margin-left: 10rpx;
		border-radius: 20rpx;
		line-height: 22rpx;
	}
	
	.icon-nv {
		background-color: #FF698D !important;
	}
</style>
