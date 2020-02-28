<template>
	<view class="body">
		<input type="password" class="uni-input common-input" placeholder="输入旧密码" />
		<input type="password" class="uni-input common-input" placeholder="输入新密码" />
		<input type="password" class="uni-input common-input" placeholder="输入确认密码" />
		<button type="primary" class="user-set-btn user-set-btn-disable">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style>
	/* css 引入需要放到第一行 */
	@import url("../../common/form.css");
</style>
