<template>
	<view class="load-more">{{loadtext}}</view>
</template>

<script>
	export default {
		props: {
			loadtext: String,
		},
		data() {
			return {

			};
		}
	}
</script>

<style scoped>
	.load-more {
		text-align: center;
		color: #AAA;
		padding: 10rpx;
	}
</style>
