<template>
	<view>
		<!-- 状态栏：使用状态栏进行占位，空出状态栏的位置 -->
		<uni-status-bar bgcolor="#FFE933"></uni-status-bar>
		登录页面
	</view>
</template>

<script>
	// 状态栏
	import uniStatusBar from "../../components/uni-status-bar/uni-status-bar.vue"
	
	export default {
		components: {
			uniStatusBar,
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

</style>
