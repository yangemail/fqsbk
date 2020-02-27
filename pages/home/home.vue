<template>
	<view>
		我的
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		onNavigationBarButtonTap(e) {
			console.log("Menu button is tapped (index): " + e.index);
			switch (e.index) {
				case 0:
					console.log("跳转到设置页面");
					break;
				default:
					break;
			}
		},
		methods: {

		}
	}
</script>

<style>

</style>
